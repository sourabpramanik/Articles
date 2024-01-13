Hello everyone, Sourab here.

Today I am going to explore [SurrealDB](https://surrealdb.com/) by creating a simple application using [NextJS](https://nextjs.org/) in which user can login and can access the protected dashboard page. 

In this project I am going to create user authentication using [NextAuth](https://next-auth.js.org/) and all the user details will be stored in SurrealDB. I will be using [Shadcn](https://ui.shadcn.com/) UI component for building the login page and dashboard page. 

So let's get started

## Create a NextJS project
Create a new NextJS project using the below command
```bash
npx create-next-app@latest nextjs-nextauth-surrealdb --typescript --tailwind --eslint
```
Select the following option in the prompt
```bash
Would you like to use `src/` directory? No
Would you like to use App Router? (recommended) Yes
Would you like to customize the default import alias (@/*)? Yes
What import alias would you like configured? @/*
```
Go inisde the project
```bash
cd nextjs-nextauth-surrealdb
```

## Setup Shadcn in the project
To setup shandcn in your NextJS project run the below command
```bash
npx shadcn-ui@latest init
```

Select the following options when prompted
```bash
Would you like to use TypeScript (recommended)? yes
Which style would you like to use? › Default
Which color would you like to use as base color? › Zinc
Where is your global CSS file? › › app/globals.css
Do you want to use CSS variables for colors? › yes
Are you using a custom tailwind prefix eg. tw-? (Leave blank if not) ...
Where is your tailwind.config.js located? › tailwind.config.ts
Configure the import alias for components: › @/components
Configure the import alias for utils: › @/lib/utils
Are you using React Server Components? › yes
```
Add all the required components using the below command
```bash
npx shadcn-ui@latest add button form dropdown-menu
```
Add lucide-react for icons 
```bash
npm install lucide-react
```
## Run SurrealDB server using docker
```bash
docker run --rm --pull always -p 8000:8000 -u root  -v /local-dir:/container-dir surrealdb/surrealdb:latest start --auth --user root --pass root file:/container-dir/dev.db
```
Now the SurrealDB server is running on port 8000. The database name is **dev**, username is **root** and password is also **root** for this demo. 

The above docker command has a docker folder specified which will let SurrealDb server use on-disk storage to store and persist any data.  

## Add NextAuth and configure SurrealDB in our NextJS project

To setup NextAuth I will install some packages

```bash
npm install next-auth
npm install @auth/surrealdb-adapter surrealdb.js
```
In lib directory create a new file surrealdb.ts and add the below code
```typescript
import { Surreal } from "surrealdb.js";

const connectionString = "http://0.0.0.0:8000"
const user = "root"
const pass = "root"
const ns = "dev"
const db = "dev"

const clientPromise = new Promise<Surreal>(async (resolve, reject) => {
    const database = new Surreal();
    try {
        await database.connect(`${connectionString}/rpc`, {
            ns, db, auth: { user, pass }
        })
        resolve(database)
    } catch (e) {
        reject(e)
    }
})
export default clientPromise
```

This configuration will connect the application to SurrealDB instance running on port 8000.

In app/api/auth create [...nextauth] directory and inside that directory create route.ts file

