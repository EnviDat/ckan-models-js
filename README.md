# ckan-models-js

JS models for CKAN-based database.

## Usage

```bash
npm install @envidat/ckan-models

# Example with top-level await (>es2022)
import { createContext } from '@envidat/ckan-models'
const { prisma } = await createContext()

# Example within async function (no top-level await)
import { createContext, ckan_package } from '@envidat/ckan-models'
# model type can also be imported, e.g. ckan_package model
const getPackages = async (request, reply) => {
  try {
    const { prisma } = await createContext()
    const packages: Array<ckan_package> = await prisma.ckan_package.findMany();
    // console.log('Retrieved successfully all packages');
    return packages;
  } catch (err) {
    console.log(err);
    return reply.status(500).send("Error: failed to retrieve packages");
  }
};
```

## Updating Models

- Clone this repo.
- Run scripts:
    ```bash
    npm run db:introspect
    npm run db:generate
    ```
- Edit package.json version & commit changes.
- Create a tag and push.
- The CI pipeline should publish to NPM.
