# Corner of Good Food

A web application for restaurants, covering table reservations and food delivery. It is built on the MEAN stack (MongoDB, Express, Angular, Node.js). The interface is in Serbian; the original name is "Kutak dobre hrane".

There are three kinds of users, and each gets a different set of pages.

**Guest**
- registers and waits for an admin to approve the account
- browses and searches restaurants and sees them on a map
- reserves a table, either through a form or by picking a table on a drawing of the restaurant floor
- orders food for delivery from the menu, using a cart
- rates and comments on a restaurant after a visit

**Waiter**
- accepts or rejects reservations for their restaurant
- handles delivery orders and sets the estimated delivery time
- sees statistics about guests and reservations as charts

**Admin**
- approves or rejects registration requests, and deactivates accounts
- adds waiters
- adds restaurants, including a floor plan with tables that is later drawn on a canvas

Everyone can edit their profile, upload a profile picture and change their password. A forgotten password is reset with a security question.

## Tech

- Angular 16 with Bootstrap, Leaflet for maps and Chart.js for statistics
- Node.js and Express in TypeScript, Mongoose for the database, Multer for image upload
- MongoDB

## Layout

```
src_frontend/   Angular sources (the src folder of the Angular project)
src_backend/    Express server: routers, controllers, models
Database/       collections exported as JSON
Images/         profile pictures and menu photos used by the sample data
```

## Running it

The repo holds the source folders, not complete project scaffolding, so there are a few manual steps.

1. **Database.** Start MongoDB on the default port and import the files from `Database/` into a database called `KutakDobreHrane`. Each file is one collection:

   ```
   mongoimport --db KutakDobreHrane --collection users --jsonArray --file Database/users.json
   ```

   Do the same for `restorani`, `rezervacije`, `narudzbine` and `zahtevi`.

2. **Backend.** In a Node project with TypeScript, install `express`, `cors`, `mongoose` and `multer`, and use `src_backend` as the source folder. Copy `Images/slike` and `Images/jelovnikSlike` next to it, since the server serves pictures from those two folders. Compile and start `server.ts`. It listens on port 4000.

3. **Frontend.** Create an Angular 16 project and replace its `src` folder with `src_frontend`. `package.json` in the repo root lists the dependencies, and `biblioteke za instaliranje.txt` has the extra installs along with the Bootstrap line for `angular.json`. Start it with `ng serve` and open `http://localhost:4200`.

The frontend expects the backend at `http://localhost:4000`.
