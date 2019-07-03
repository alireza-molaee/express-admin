![NPM](https://img.shields.io/npm/l/express-cool-admin.svg)
[![FOSSA Status](https://app.fossa.com/api/projects/git%2Bgithub.com%2Falireza-molaee%2Fexpress-admin.svg?type=shield)](https://app.fossa.com/projects/git%2Bgithub.com%2Falireza-molaee%2Fexpress-admin?ref=badge_shield)

# express-cool-admin
A backend library for building admin applications running in the browser on top of express. It dose not depend on any database or orm.Open sourced and maintained by Alireza.

# Features
- Adapts to any database
- Supports relationships by query field
- Custom actions
- Supports authentication with session apart from your user and your auth
- cool ui

# Installation
React-admin is available from npm. You can install it (and its required dependencies) using:

```
npm i express-cool-admin
```
# Usage

import expressAdmin and use that like below:
```es6
// app.js
import express from 'express';
import expressAdmin from 'express-cool-admin';
import { userAdmin, carAdmin, companyAdmin } from './admin.js';

const app = express();

const config = {
    entities: [userAdmin, carAdmin, companyAdmin]
}

app.use('/admin', expressAdmin(config));
```
each entity most have schema like below:

```es6
// admin.js
export const userAdmin = {
    slug: 'user', // it used for url
    title: 'User', // it will shown to user
    icon: 'users', // font awesome icon name
    fields: { // data schema
        firstName: {
            type: 'text',
            title: 'First Name'
        },
        lastName: {
            type: 'long-text',
            title: 'Last Name'
        },
        phoneNumber: {
            type: 'number',
            title: 'Phone Number'
        },
        isActive: {
            type: 'bool',
            title: 'Is Active',
        },
        joinAt: {
            type: 'date',
            title: 'Join At',
            options: {
                format: 'YYYY/MM/DD HH:mm',
            }
        },
        role: {
            type: 'enum',
            title: 'Role',
            options: {
                map: {
                    'admin': 'Admin',
                    'manager': 'Manager',
                    'manager-assistant': 'Manager Assistant',
                },
                inputType: 'radio-inline',
            }
        },
        permissions: {
            type: 'multi-enum',
            title: 'Permissions',
            options: {
                map: {
                    'admin': 'Admin',
                    'manager': 'Manager',
                    'manager-assistant': 'Manager Assistant',
                },
                inputType: 'check-box-inline',
            }
        },
        picture: {
            type: 'file',
            title: 'Picture',
            options: {

            }
        },
        car: {
            type: 'query-multiple',
            title: 'Car',
            options: {
                onQuery: (q, page) => {
                    return {
                        "results": [
                            {
                            "id": '1',
                            "text": "Option 1"
                            },
                            {
                            "id": '2',
                            "text": "Option 2"
                            },
                            {
                            "id": '3',
                            "text": "Option 3"
                            }
                        ],
                        "pagination": {
                            "more": false
                        }
                    }
                },
                getLabel: (id) => {
                    return {
                        id,
                        text: 'Option ' + id
                    }
                }
            }
        }
    },
    listViewFields: ['firstName', 'lastName', 'phoneNumber', 'isActive', 'joinAt', 'role', 'permissions', 'picture'],
    listViewActions: [
        {
            id: 'delete-all',
            title: 'delete all',
        },
        {
            id: 'confirm-all',
            title: 'confirm all',
        },
        {
            id: 'suspend-all',
            title: 'suspend all',
        }
    ],
    onTriggerAction: (actionId, selectedItems) => {

    },
    getListItems: (page, filters) => {
        return {
            items: [ // this data could be provided from every where
            {
                _id: '1',
                firstName: 'foo',
                lastName: 'bar',
                phoneNumber: '09121010101',
                isActive: true,
                joinAt: new Date(),
                role: 'admin',
                permissions: ['admin', 'manager'],
                picture: 'http://lorempixel.com/200/200/people/'
            },
            {
                _id: '2',
                firstName: 'foo',
                lastName: 'bar',
                phoneNumber: '09121010101',
                isActive: true,
                joinAt: new Date(),
                role: 'admin',
                permissions: ['admin', 'manager'],
                picture: 'http://lorempixel.com/200/200/people/'
            },
            {
                _id: '3',
                firstName: 'foo',
                lastName: 'bar',
                phoneNumber: '09121010101',
                isActive: false,
                joinAt: new Date(),
                role: 'admin',
                permissions: ['admin', 'manager'],
                picture: 'http://lorempixel.com/200/200/people/'
            },
            {
                _id: '4',
                firstName: 'foo',
                lastName: 'bar',
                phoneNumber: '09121010101',
                isActive: false,
                joinAt: new Date(),
                role: 'admin',
                permissions: ['admin', 'manager'],
                picture: 'http://lorempixel.com/200/200/people/'
            },
            {
                _id: '5',
                firstName: 'foo',
                lastName: 'bar',
                phoneNumber: '09121010101',
                isActive: true,
                joinAt: new Date(),
                role: 'admin',
                permissions: ['admin', 'manager'],
                picture: 'http://lorempixel.com/200/200/people/'
            }
            ],
            totalPage: 6, 
        }  
    },
    getItem: (id) => {
        return { // this data could be provided from every where
            firstName: 'foo',
            lastName: 'bar',
            phoneNumber: '09121010101',
            isActive: true,
            joinAt: new Date(),
            role: 'admin',
            permissions: ['admin', 'manager'],
            picture: 'http://lorempixel.com/200/200/people/',
            car: ['2', '1'],
        }
    },
    addItem: (data) => {
        console.log(data);
        return 1;
    },
    editItem: (id, data) => {
        console.log(id, data);
        return 1
    },
    deleteItem: (id) => {
        return 1
    }
}
```

finally you can make admin db with [make-admin-db script](scripts/make-admin-db.js) and add admin user with [add-user-to-admin script](scripts/add-user-to-admin.js)

# Contributing
Pull requests are welcome on the GitHub repository. Try to follow the coding style of the existing files, and include unit tests and documentation. Be prepared for a thorough code review, and be patient for the merge - this is an open-source initiative.

# License
express-cool-admin is licensed under the MIT Licence, sponsored and supported by Alireza molaee.



