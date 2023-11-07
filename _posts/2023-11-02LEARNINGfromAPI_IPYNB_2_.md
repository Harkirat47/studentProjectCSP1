---
toc: True
comments: True
layout: post
title: Learning from past mistakes
type: tangibles
courses: {'csp': {'week': 11}}
---

# MISTAKES TO AVOID AND FIX IN THE API

### Delete the squlite table to reset meta data on nighthawk coders

this is because we ran into read and write errors quite frequently when trying to restart our server.
SQlite regenerates when rerun



### PYTHON MAIN.PY

Most releiable method to run, more than docker in my opinion


### CORS, disable cors for pull requests, I do not have a long term fix yet

### Data best stored in a dictionary, 

code to always use to get data

 fetch(apiUrl)
            .then(response => response.json()) // Parse the JSON response
            .then(data => {
                // Organize the data into a dictionary
                const organizedData = {
                    Cookie_api: {
                        url_prefix: '/api/Cookie',
                        CookieAPI: {
                            get: {
                                description: 'Retrieve all cookies from the database',
                                url: '/api/Cookie',
                                method: 'GET',
                                data: data, // Include the retrieved data here
                            },
                        },
                    },
                    CookieListAPI: {
                        CookieListAPI: {
                            get: {
                                description: 'Retrieve all cookies from the database',
                                url: '/api/Cookie',
                                method: 'GET',
                                data: data, // Include the retrieved data here
                            },
                        },
                    },
                };

                // Now, you have the organized data in the "organizedData" dictionary
                Data = organizedData.Cookie_api.CookieAPI.get.data; //data[id].Cookie_name, image whatever u may need,

# always use a db system
