# Travel Forum - Frontend

**Author:** Kris Sakarias

**Version** 1.0.0


## Overview

This is a front-end travel forum application. Users can navigate to regional forums to post and comment on different topics of discussion related to a travel destination. There is also a chat room for quick interaction between users who are online. 

The forum is built with *React* and *Redux*, with *Babel* and *Webpack*. The chat room is built with *Socket.io*


## Documentation 

### Component Architecture

A mixture of class and functional components are used. Generally components that are connected to Redux are classes, and components that are reused multiple times are functional.

```
Landing -> Auth Form
Header -> Chat Room
   |
Continent Container -> Table Template -> Trends Box -> Country Menu
   |
Country Container -> Table Template -> Trends Box -> Post Form
   |                                                    |
Thread Container -> Post Template -> Post Form          |
   |                                     |________ Modal Container -> Post Form
   |                                                                  Delete Modal
   |
Profile View
```

### Components

**Base Components**

`Landing`
- Displays list of regional subforums
- Select a regional subforum...

`Continent Container`
- Displays list of country subforums within regional (continent) subforum
- Shows total threads in each country, ordered by most recently active

`Country Container`
- Displays list of threads in a country's subforum
- Shows total comments per thread, ordered by most recently active

`Thread Container`
- Displays selected thread and comments

**Profile View**
- Shows selected profile's basic stats


**Child Components**

`Header`

*Parent Components:* All, except Chat Room
- Navigation to `Auth Form`, `Profile View`, and `Chat Room`

`Country Menu`

*Parent Component*: `Continent Container`
- Dropdown list to initialize a country subforum that is not currently active

`Trend Box`

*Parent Components*: `Continent Container`, `Country Container`
- Shows trending countries or threads based on recent activity 

`Post Form`

*Parent Components*: `Country Container`, `Thread Container`
- Post a new thread or comment

