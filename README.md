# Open Food Products API

This is a free, self-hostable API about food products (Branded Food Products
Database) from the [USDA](https://www.ars.usda.gov/northeast-area/beltsville-md-bhnrc/beltsville-human-nutrition-research-center/nutrient-data-laboratory/docs/usda-branded-food-products-database/), collected via public-private partnership. Included are
~2.3 million food products, their manufacturer, UPC number, ingredients, and
also nutritional information. Up to date as of Jan 2018.

Powered by [postgrest](https://github.com/PostgREST/postgrest), because I already cleaned up and put together a postgres database based on information from the BFDL database from USDA.

## Usage

1.  Install [Docker](https://www.docker.com/products/docker-desktop)

2.  Make `db.env` and `postgrest.env`. There are example files: `db.env.example`
    and `postgrest.env.example`. You can set your own db password by replacing
    `[password]` with the right value.

3.  Run `docker-compose up` to launch everything. On first launch, it'll take
    about 30 to 60 seconds to fully seed itself with `db/food_products.sql.zip`.

4.  Now, you can visit http://localhost:3000 in a web browser!

If Docker is too annoying to use, just grab `./db/food_products.sql.zip` -- it's
a full Postgres database dump. Also, [`postgrest`](http://postgrest.org) could
be used natively as well –– it's an application you can download and run.

## Documentation

[Docs about postgrest.](http://postgrest.org/en/v5.2/install.html#configuration)

API docs are at `http://localhost:3000`. Only read access is provided over a
REST interface, and the data is provided as JSON. There are a number of very
flexible filters available too! And `postgrest` enables great performance on
crappy hardware.

Example query using full text search (phrase-based –– see docs above):

```
http://localhost:3000/food_products?q=plfts.ice+cream
```

## Of Interest

- `db/Dockerfile` is relevant if you want to see how to make a Docker image that self-seeds with data on launch (no db setup steps for dev/CI/test environment!)
- `db/food_products.sql.zip` is a Postgres database dump

## License

MIT. See `./LICENSE`.
