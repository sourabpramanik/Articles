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



