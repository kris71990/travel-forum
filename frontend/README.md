# Travel Forum - Frontend

<img src="src/assets/flag-banner.png">

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
