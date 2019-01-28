# Open Food Products API

This is a free, self-hostable API about food products (Branded Food Products
Database) from the [USDA](https://www.ars.usda.gov/northeast-area/beltsville-md-bhnrc/beltsville-human-nutrition-research-center/nutrient-data-laboratory/docs/usda-branded-food-products-database/), collected via public-private partnership. Included are
~240K food products, their manufacturer, UPC number, ingredients, and
also nutritional information. Up to date as of Jan 2019.

Powered by [postgrest](https://github.com/PostgREST/postgrest), because I already cleaned up and put together a postgres database based on information from the BFDL database from USDA.

**Demo API** running on a \$5 Digital Ocean droplet: https://open-food-api-demo.kilotau.com/.

**Example queries:**

- using full text search: https://open-food-api-demo.kilotau.com/food_products?q=plfts.ice+cream
- using the equivalent of `foo LIKE '%bar%`: https://open-food-api-demo.kilotau.com/food_products?ingredients=like.*egg*
- using a date field: https://open-food-api-demo.kilotau.com/food_products?date_available=gt.2018-06-01

API documentation is at [root](https://open-food-api-demo.kilotau.com/). And more general information about filters/parameters is [here in postgrest's docs](http://postgrest.org/en/v5.2/api.html#).

## Usage

1.  Install [Docker](https://www.docker.com/products/docker-desktop)

2.  Download [`food_products.sql.zip`](https://www.dropbox.com/s/e666mk2aj4lf6ve/food_products.sql.zip?dl=0) to `./db/food_products.sql.zip`

3.  Make `db.env` and `postgrest.env`. There are example files: `db.env.example`
    and `postgrest.env.example`. You can set your own db password by replacing
    `[password]` with the right value.

4.  Run `docker-compose up` to launch everything. On first launch, it'll take
    about 30 to 60 seconds to fully seed itself with `db/food_products.sql.zip`.

5.  Now, you can visit http://localhost:3000 in a web browser!

If Docker is too annoying to use, just grab `./db/food_products.sql.zip` -- it's
a full Postgres database dump. Also, [`postgrest`](http://postgrest.org) could
be used natively as well –– it's an application you can download and run.

## Documentation

[Docs about postgrest.](http://postgrest.org/en/v5.2/install.html#configuration)

API docs are at `http://localhost:3000`. Only read access is provided over a
REST interface, and the data is provided as JSON. There are a number of very
flexible filters available too! And `postgrest` enables great performance on
crappy hardware.

## Of Interest

- `db/Dockerfile` is relevant if you want to see how to make a Docker image that self-seeds with data on launch (no db setup steps for dev/CI/test environment!)
- `db/create_readonly_role.sql` does what it says –– but it was embarassingly
  tricky to find out all I needed to do for such a role. Hoping it saves you
  time.

## License

MIT. See `./LICENSE`.
