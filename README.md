# Celestial Bodies Database

A relational PostgreSQL database that models the universe: galaxies, the stars inside them, the planets orbiting those stars, and the moons orbiting those planets.

## Tech used

PostgreSQL · SQL

## Database structure

| Table | Rows | Description |
|---|---|---|
| `galaxy` | 6 | Galaxies such as the Milky Way and Andromeda |
| `star` | 6 | Stars, each linked to a galaxy |
| `planet` | 12 | Planets, each linked to a star |
| `moon` | 20 | Moons, each linked to a planet |
| `planet_types` | 3 | Reference table of planet types |

The tables are connected through foreign keys:

```
galaxy ──< star ──< planet ──< moon
```

## Features

- Auto-incrementing primary keys following the `table_name_id` convention
- Foreign keys linking each moon to a planet, each planet to a star, and each star to a galaxy
- `NOT NULL` and `UNIQUE` constraints on every table
- A range of data types: `INT`, `NUMERIC`, `TEXT`, `BOOLEAN` and `VARCHAR`

## How to run it

Rebuild the database from the dump file:

```bash
psql -U postgres < universe.sql
```

Then connect and explore:

```bash
psql -U postgres -d universe
```

```sql
SELECT moon.name, planet.name AS planet
FROM moon
INNER JOIN planet ON moon.planet_id = planet.planet_id
ORDER BY planet.name;
```

## What I learned

- Designing a relational schema from requirements
- Choosing appropriate data types and constraints
- Creating one-to-many relationships with foreign keys
- Inserting data in the right order so every reference is valid
