---
layout: post
title:      "`form_tag` vs. `from_for`, What to expected with `form_with` "
date:       2020-11-04 09:47:52 +0000
permalink:  form_tag_vs_from_for_what_to_expected_with_form_with
---



`form_tag` and `form_for` provide two very similiar interfaces to much of the same thing. Keeping with the DRY principle,  repetition is shunned upon and soon `form_tag` and `form_for` will be depricated and replaced with with `form_with`. 


`form_tag` is used to create forms where there is no underlying model. 


```
<%= form_tag users_path do %>
  <%= text_field_tag :email %>
  <%= submit_tag %>
<% end %>
```

`form_for` is used when you have model. 

```
<%= form_for @user do |form| %>
  <%= form.text_field :email %>
  <%= form.submit %>
<% end %>
```


here is an example for `form_with` without a model. 

```
<%= form_with url: users_path do |form| %>
  <%= form.text_field :email %>
  <%= form.submit %>
<% end %>
```

Here is an example with a model

```
<%= form_with model: @user do |form| %>
  <%= form.text_field :email %>
  <%= form.submit %>
<% end %>
```

Setting the `model` argument then `scope` and `url` are automatically derived from it. this pattern is derived from  `form_for`.


The diffference in syntax between the two examples provided above is that `form_for` uses form builder helpers making `form_tag` a little more efficient in regards to the amount of code required to complete a form. `form_with` will provide form builders. 



The unification of usage and subsequent calls to field tags will simplify how you build your forms. Additionally, from_with solves some deficiencies with the current helpers.





