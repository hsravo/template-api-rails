# Template API Rails
Template initialement forked depuis https://github.com/jameschambers/boring-bits-rails-api
Modifications faites sur la class JwtDenylist
Reste à modifier la migration CreateJwtDenylist :

**Remplacer le code de la migration db/migrate/create_jwt_denylist.rb par ce qui suit :**

```
class CreateJwtDenylist < ActiveRecord::Migration[6.0]
  def change
    create_table :jwt_denylist do |t|
      t.string :jti, null: false
      t.datetime :exp, null: false
    end
    add_index :jwt_denylist, :jti
  end
end
```
**Puis reconstruire la db (car on a modifié une migration !)**
Ceci sera mis à jour prochainement pour que le template s'occupe de tout !

Enjoy !


# 😴 Boring Bits: Rails API Edition

**A bare-bones Rails 6 template for API-only applications which use JWT authentication.** 

It's not glamourous. It's not sexy. It's just a dependably Boring starting point for your next API.

Plays nicely with [Boring Bits: Nextjs Edition](https://github.com/jameschambers/boring-bits-nextjs).

## Highlights

- Devise auth with JSON Web Tokens (JWT)
- Login, signup, and protected route examples
- JSON:API response rendering
- Namespaced /api/ routes
- TDD-ready with passing Rspec tests

## Getting started

Ensure you have Ruby 2.6.x and Rails 6 installed on your machine.

Clone this repository, then specify your local path to `template.rb` with the `-m` flag: 

``` 
$ rails new YourAppName --api -m ../local/path/to/template.rb
```

The template will install all necessary gems, and create a new database for you. Check everything is installed correctly by cd-ing into `YourAppName`, then running the specs with: 

```
$ foreman run rake
```

## Making API calls

API calls are authenticated with JWT tokens taken from the `Authorization` header. See `spec/controllers/user_controller_spec.rb` for an example. 

`Authorization` headers are returned by login and signup routes, so you need to save the header value client-side, then include that header with your subsequent API requests. 

