Universe Database Project

This project is part of the FreeCodeCamp Relational Database Certification. The goal of this project is to create a PostgreSQL database that models a simplified version of the universe, containing tables for galaxies, stars, planets, moons, and asteroids. The database is designed to meet several specific requirements, such as the inclusion of certain data types, foreign keys, and primary keys, while allowing for creativity in the design.

Project Structure

The database consists of five primary tables:

    1. galaxy - Stores data about various galaxies in the universe.

    2. star - Stores data about stars and their relation to galaxies.

    3. planet - Stores data about planets and their relation to stars.

    4. moon - Stores data about moons and their relation to planets.

    5. asteroid - Stores data about asteroids.
##  Table Details

    1.galaxy:

    galaxy_id (SERIAL PRIMARY KEY)
    name (VARCHAR(100) UNIQUE, NOT NULL)
    age_in_millions_of_years (INT, NOT NULL)
    is_spherical (BOOLEAN, NOT NULL)
    distance_from_earth (NUMERIC, in millions of light years)
    description (TEXT)

    2.star:

    star_id (SERIAL PRIMARY KEY)
    name (VARCHAR(100) UNIQUE, NOT NULL)
    age_in_millions_of_years (INT, NOT NULL)
    is_spherical (BOOLEAN, NOT NULL)
    galaxy_id (INT, FOREIGN KEY references galaxy table)

    3.planet:

    planet_id (SERIAL PRIMARY KEY)
    name (VARCHAR(100) UNIQUE, NOT NULL)
    has_life (BOOLEAN, NOT NULL)
    distance_from_star (NUMERIC, distance in AU)
    star_id (INT, FOREIGN KEY references star table)

    4.moon:

    moon_id (SERIAL PRIMARY KEY)
    name (VARCHAR(100) UNIQUE, NOT NULL)
    is_spherical (BOOLEAN, NOT NULL)
    distance_from_planet (NUMERIC, distance in AU)
    planet_id (INT, FOREIGN KEY references planet table)


    5.asteroid:

    asteroid_id (SERIAL PRIMARY KEY)
    name (VARCHAR(100) UNIQUE, NOT NULL)
    is_spherical (BOOLEAN, NOT NULL)
    size_in_km (NUMERIC, size in kilometers)
    composition (TEXT)
## Features

Primary and Foreign Keys: 

    Each table has a primary key that is automatically incremented. The relationships 
    between galaxies, stars, planets, and moons are established using foreign keys.

Data Types:

    The TEXT data type is used in the description and composition columns.
    The BOOLEAN data type is used to track whether objects are spherical or support
    life.
    The NUMERIC data type is used for distances and sizes.

Constraints:

    Certain columns, such as name, are set to be unique and cannot be NULL.
    Foreign key constraints are used to ensure data integrity across related tables.
## Example Queries
Here are some example queries you can use to explore the database:

List all galaxies with their descriptions:

    SELECT name, description FROM galaxy;

Get all planets that are part of a specific star system:

    SELECT planet.name 
    FROM planet
    JOIN star ON planet.star_id = star.star_id
    WHERE star.name = 'Sun';

Find all moons of a specific planet:

    SELECT moon.name 
    FROM moon
    JOIN planet ON moon.planet_id = planet.planet_id
    WHERE planet.name = 'Earth';

Show details of all asteroids with their composition:

    SELECT name, size_in_km, composition 
    FROM asteroid;