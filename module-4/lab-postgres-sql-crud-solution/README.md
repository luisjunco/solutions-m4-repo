![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | PostgreSQL CRUD

<details>
  <summary>
   <h2>Learning Goals</h2>
  </summary>

This exercise allows you to practice and apply the concepts and techniques taught in class.

Upon completion of this exercise, you will be able to:

- Perform CRUD operations on a PostgreSQL database by using SQL statements
- Use SQL logical operators to conditionally retrieve database records

  <br>

  <hr>

</details>

## Introduction

We just learned about databases and SQL. Now let's put that knowledge into practice!

In this lab, you will practice SQL by working with a PostgreSQL database. You will use the `psql` client to execute SQL queries to create, read, update, and delete records in a database.

<br>


## Requirements

- Fork this repo
- Clone this repo

<br>

## Submission

- Upon completion, run the following commands

```
$ git add .
$ git commit -m "done"
$ git push origin master
```

- Create a Pull Request and submit your assignment.

<br>

## Deliverables

Since we will be querying our database from `psql`, you will need to copy/paste the query you entered in `psql`.

In the `queries.md` file, you will find the instructions about the query you need to perform in each iteration and a space to fill the answer.


### Example

Here is an example of how you should paste your SQL queries in the `queries.md` file for each iteration:

Find all technologies in the database:

```sql
#  This should be pasted in the queries.md file
SELECT * FROM technologies;
```

<br>

## Iteration 1 - Setup

First, we need to create a database table we will be using during the lab and add some data to it. We will work with a table containing information about JavaScript libraries that we will name **`jslibraries`**.

To create a new table named `jslibraries` and add records to it, run the below queries in the `psql` client:

```sql
CREATE TABLE jslibraries(
    name            VARCHAR(17),
    owner           VARCHAR(17),
    description     VARCHAR(113),
    stars           INTEGER,
    url             VARCHAR(42),
    releases        INTEGER,
    licence         VARCHAR(11),
    used_by         INTEGER,
    contributors    INTEGER,
    main_technology VARCHAR(10),
    type            VARCHAR(18),
    release_date    DATE
);

INSERT INTO jslibraries(name, owner, description, stars, url, releases, licence, used_by, contributors, main_technology, type,release_date)
VALUES
  ('react', 'facebook', 'A declarative, efficient, and flexible JavaScript library for building user interfaces.', 174000,'reactjs.org', 138, 'MIT License', 7400000, 1501, 'javascript', 'SPA library', '2014-08-23'),
  ('vue', 'vuejs', 'A Vue.js is a progressive, incrementally-adoptable JavaScript framework for building UI on the web.', 188000, 'vuejs.org', 252, 'MIT License', NULL, 399, 'javascript', 'SPA library', '2016-05-30'),
  ('styled-components', 'styled-components', 'Visual primitives for the component age. Use the best bits of ES6 and CSS to style your apps without stress.', 34600, 'styled-components.com', 195,'MIT License',731000,288,'typescript','CSS-in-JS Library','2016-06-18'),
  ('ant-design', 'ant-design','VAn enterprise-class UI design language and React UI library.',34600,'ant.design',474,'MIT License',233000,1469,'typescript','Components Library','2012-12-16'),
  ('chakra-ui','chakra-ui', '⚡️ Simple, Modular & Accessible UI Components for your React Applications.', 20300, 'chakra-ui.com', 2073, 'MIT License', 23100, 429, 'typescript', 'Components Library', '2018-08-12'),
  ('victory', 'FormidableLabs', 'A collection of composable React components for building interactive data visualizations.', 9100, 'http://formidable.com/open-source/victory/', 214 ,NULL, 9700, 148, 'javascript', 'Charts Library', '2014-08-08'),
  ('pug', 'pugjs', 'Pug – robust, elegant, feature rich template engine for Node.js.', 20300, 'pugjs.org', 244, 'MIT License', 348000, 253, 'javascript', 'Template engine', '2012-02-07'),
  ('hbs', 'pillarjs', 'Express view engine wrapper for Handlebars.', 1500, 'pugjs.org', 44, 'MIT License', NULL, 25, 'javascript', 'Template engine', '2013-08-25'),
  ('bootstrap', 'twbs', 'The most popular HTML, CSS, and JavaScript framework for developing responsive, mobile first projects on the web.', 153000, 'getbootstrap.com', 72, 'MIT License', 2700000, 1240, 'javascript', 'CSS Framework', '2017-10-25'),
  ('materialize', 'Dogfalo', 'Materialize, a CSS Framework based on Material Design.', 36600, 'materializecss.com', 44, 'MIT License', 77200, 261, 'javascript', 'CSS Framework', '2016-08-20'),
  ('moment', 'moment', 'Parse, validate, manipulate, and display dates in javascript.', 45900, 'momentjs.com', 84, NULL, 2500000, 590, 'javascript', 'Date library', '2012-10-08')


```

If throughout the lab you delete or change something accidentally, you can always drop the `jslibraries` table and recreate it again by running the above queries.

<br>

## Iteration 2

You already know how this goes, so let's start running some queries on our database.

1. Add the **solid** and **chartjs** libraries as new rows to the `jslibraries` table. Use the below data for the new rows:

```js
[
  {
    name: 'solid',
    owner: 'solidjs',
    description: 'A declarative, efficient, and flexible JavaScript library for building user interfaces.',
    stars: 10700,
    url: 'solidjs.com',
    releases: 194,
    licence: 'MIT License',
    used_by: 624,
    contributors: 73,
    main_technology: 'typescript',
    type: 'UI Library',
    release_date: '2011-08-13'
  },
  {
    name: 'chartjs',
    owner: 'chartjs',
    description: 'Simple HTML5 Charts using the canvas tag.',
    stars: 54700,
    url: 'chartjs.org',
    releases: 85,
    licence: 'MIT License',
    used_by: 414000,
    contributors: 377,
    main_technology: 'javascript',
    type: 'Charts Library',
    release_date: '2011-11-02'
  }
];
```

<br>

2. Get **all the fields** of the library that was **released earliest** (first). <br> <br>
3. Get **all the fields** of the library that was **released most recently** (last). <br> <br>
4. All the libraries released **before 2015**. <br> <br>
5. Get the `name` and the `release_date` of the libraries **without a licence**. <br> <br>
6. Get the `name` and the `stars` from all **CSS Framework** libraries. <br> <br>
7. Get the `name` of the libraries where the main technology is **Typescript**. <br> <br>
8. Get the `name` and the `type` of all the libraries with **more than 1000 contributors**. <br> <br>
9. Get the **total** number of `stars` of **all the libraries**. <br> <br>
10. Get the **average** number of `contributors` for **all the libraries**. <br> <br>
11. Update the `licence` field of the **libriaries without a licence** to store `'unknown'` instead of `NULL`. <br> <br>
12. Update the `used_by` field of the **libraries that don't have it specified** to store `'unknown'` instead of `NULL`. <br> <br>
13. Update all the records to **capitalize the string** provided in the `main_technology` field. <br> <br>
14. Delete all the records where `licence` is `'unknown'`. <br> <br>
15. Delete all the records with **10000 or less** `stars`. <br> <br>
16. Delete all the records with **less than 100** `releases`. <br> <br>

Happy Coding! 💙
