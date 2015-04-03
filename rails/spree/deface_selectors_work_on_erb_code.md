# Deface selectors work on erb code

So Spree has this gem called Deface (https://github.com/spree/deface) which lets the developers
inject stuff into a Spree view without overwriting the whole file.

In short, you select whether it should insert stuff before/after an element, replace it/remove it
altogether etc.

### How to find an element to replace

Finding an element is easy because it uses Nokogiri's implementation of css selectors.

### My problem

Our client asked us to make the emails in a certain table be links to a user's profile instead of a
`mailto:` link as it is in Spree.

Quick look at the Erb code:

```
<table>
  ...
  <tbody>
    ...
    <tr data-hook="admin_orders_index_rows" class="some-dynamic-class">
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td><%= mail_to order.email %></td> <- That's the bit we want to replace
    </tr>
  </tbody>
</table>
```

Unfortunately, the `<td>` had no class so we need a pseudo selector to find it. Here is the
selector that I thought would work.

`tr[data-hook=admin_orders_index_rows] td:nth-of-type(6) a`

But here is what Deface had to say about it: `Deface: 'make_email_a_link_to_profile' matched 0 times with 'tr[data-hook=admin_orders_index_rows] td:nth-of-type(6) a'`

### Why it didn't work?

After a lot of frustration, trying different selectors, theories that Deface doesn't find `a` elements
because of a bug it turns out that

#### Deface uses the selectors on Erb files and not compiled HTML files

Moreover, you can write Deface overrides in Haml/Slim but it will still
1. Convert them to Erb
2. Convert Erb blocks into Html-ish tags
..* `<% some_method %>` = `<erb silent> some_method </erb>`
..* `<%= some_method %>` = `<erb loud> some_method </erb>`
3. Do all the overrides there

So, since we want to replace an Erb block, our selector will have to contain `erb[loud]` instead of `a`

### Final solution

```
/ replace 'tr[data-hook=admin_orders_index_rows] td:nth-of-type(6) erb[loud]'
<%= link_to order.email, admin_user_path(order.user) %>
```




