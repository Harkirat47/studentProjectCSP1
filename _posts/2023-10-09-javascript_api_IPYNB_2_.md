---
layout: post
title: JS CHart With API
description: These examples show the basic language structures and constructs of Python using input and output (print) commands.
courses: {'csp': {'week': 2}}
categories: ['C4.0']
type: hacks
---

```python
%%html
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pokémon Details Table with Pagination</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
            margin: 0;
            padding: 0;
        }

        h1 {
            text-align: center;
            margin-top: 20px;
            color: #333;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: #fff;
            margin: 20px auto;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        th, td {
            padding: 10px;
            text-align: left;
        }

        th {
            background-color: #007BFF;
            color: #fff;
        }

        tr:nth-child(even) {
            background-color: #f2f2f2;
        }

        #pagination {
            text-align: center;
            margin-top: 20px;
        }

        button {
            padding: 10px 20px;
            background-color: #007BFF;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <table id="pokemonTable">
        <thead>
            <tr>
                <th>Name</th>
                <th>Power</th>
                <th>Rarity</th>
                <th>Type</th>
                <th>Height</th>
                <th>Weight</th>
                <th>Abilities</th>
                <th>Forms</th>
                <th>Base Experience</th>
            </tr>
        </thead>
        <tbody>
            <!-- Table rows will be added dynamically -->
        </tbody>
    </table>

    <div id="pagination">
        <button id="prevPage">Previous Page</button>
        <button id="nextPage">Next Page</button>
    </div>

    <script>
        $(document).ready(function () {
            // Initialize variables
            const apiUrl = 'https://pokeapi.co/api/v2/pokemon/';
            const pageSize = 10; // Number of Pokémon to display per page
            let offset = 0;

            // Function to fetch and display Pokémon data
            function fetchPokemon(offset) {
                $.ajax({
                    url: `${apiUrl}?offset=${offset}&limit=${pageSize}`,
                    method: 'GET',
                    dataType: 'json',
                    success: function (data) {
                        // Clear existing table rows
                        $('#pokemonTable tbody').empty();

                        // Loop through the data and populate the table
                        $.each(data.results, function (index, pokemon) {
                            // Get Pokémon details
                            $.ajax({
                                url: pokemon.url,
                                method: 'GET',
                                dataType: 'json',
                                success: function (pokemonData) {
                                    const name = pokemonData.name;
                                    const power = pokemonData.stats[0].base_stat;
                                    const rarity = pokemonData.stats[5].base_stat;
                                    const type = pokemonData.types.map(t => t.type.name).join(', ');
                                    const height = pokemonData.height;
                                    const weight = pokemonData.weight;
                                    const abilities = pokemonData.abilities.map(a => a.ability.name).join(', ');
                                    const forms = pokemonData.forms.map(f => f.name).join(', ');
                                    const baseExperience = pokemonData.base_experience;

                                    // Append the Pokémon data to the table
                                    $('#pokemonTable tbody').append(`
                                        <tr>
                                            <td>${name}</td>
                                            <td>${power}</td>
                                            <td>${rarity}</td>
                                            <td>${type}</td>
                                            <td>${height}</td>
                                            <td>${weight}</td>
                                            <td>${abilities}</td>
                                            <td>${forms}</td>
                                            <td>${baseExperience}</td>
                                        </tr>
                                    `);
                                },
                                error: function (error) {
                                    console.error('Error fetching Pokémon details:', error);
                                },
                            });
                        });
                    },
                    error: function (error) {
                        console.error('Error fetching Pokémon data:', error);
                    },
                });
            }

            // Initial load of Pokémon data
            fetchPokemon(offset);

            // Function to handle pagination
            function updatePaginationButtons() {
                $('#prevPage').prop('disabled', offset === 0);
                // Assuming you want to load all Pokémon data, you can remove the next page check.
                $('#nextPage').prop('disabled', false);
            }

            // Pagination: Load the previous page
            $('#prevPage').click(function () {
                offset -= pageSize;
                if (offset < 0) {
                    offset = 0;
                }
                fetchPokemon(offset);
                updatePaginationButtons();
            });

            // Pagination: Load the next page
            $('#nextPage').click(function () {
                offset += pageSize;
                fetchPokemon(offset);
                updatePaginationButtons();
            });

            // Initial pagination button state
            updatePaginationButtons();
        });
    </script>
</body>
</html>

```


<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Pokémon Details Table with Pagination</title>
    <script src="https://code.jquery.com/jquery-3.6.0.min.js"></script>
    <style>
        body {
            font-family: Arial, sans-serif;
            background-color: #f2f2f2;
            margin: 0;
            padding: 0;
        }

        h1 {
            text-align: center;
            margin-top: 20px;
            color: #333;
        }

        table {
            width: 100%;
            border-collapse: collapse;
            background-color: #fff;
            margin: 20px auto;
            box-shadow: 0 0 10px rgba(0, 0, 0, 0.1);
        }

        th, td {
            padding: 10px;
            text-align: left;
        }

        th {
            background-color: #007BFF;
            color: #fff;
        }

        tr:nth-child(even) {
            background-color: #f2f2f2;
        }

        #pagination {
            text-align: center;
            margin-top: 20px;
        }

        button {
            padding: 10px 20px;
            background-color: #007BFF;
            color: #fff;
            border: none;
            cursor: pointer;
        }

        button:disabled {
            background-color: #ccc;
            cursor: not-allowed;
        }
    </style>
</head>
<body>
    <table id="pokemonTable">
        <thead>
            <tr>
                <th>Name</th>
                <th>Power</th>
                <th>Rarity</th>
                <th>Type</th>
                <th>Height</th>
                <th>Weight</th>
                <th>Abilities</th>
                <th>Forms</th>
                <th>Base Experience</th>
            </tr>
        </thead>
        <tbody>
            <!-- Table rows will be added dynamically -->
        </tbody>
    </table>

    <div id="pagination">
        <button id="prevPage">Previous Page</button>
        <button id="nextPage">Next Page</button>
    </div>

    <script>
        $(document).ready(function () {
            // Initialize variables
            const apiUrl = 'https://pokeapi.co/api/v2/pokemon/';
            const pageSize = 10; // Number of Pokémon to display per page
            let offset = 0;

            // Function to fetch and display Pokémon data
            function fetchPokemon(offset) {
                $.ajax({
                    url: `${apiUrl}?offset=${offset}&limit=${pageSize}`,
                    method: 'GET',
                    dataType: 'json',
                    success: function (data) {
                        // Clear existing table rows
                        $('#pokemonTable tbody').empty();

                        // Loop through the data and populate the table
                        $.each(data.results, function (index, pokemon) {
                            // Get Pokémon details
                            $.ajax({
                                url: pokemon.url,
                                method: 'GET',
                                dataType: 'json',
                                success: function (pokemonData) {
                                    const name = pokemonData.name;
                                    const power = pokemonData.stats[0].base_stat;
                                    const rarity = pokemonData.stats[5].base_stat;
                                    const type = pokemonData.types.map(t => t.type.name).join(', ');
                                    const height = pokemonData.height;
                                    const weight = pokemonData.weight;
                                    const abilities = pokemonData.abilities.map(a => a.ability.name).join(', ');
                                    const forms = pokemonData.forms.map(f => f.name).join(', ');
                                    const baseExperience = pokemonData.base_experience;

                                    // Append the Pokémon data to the table
                                    $('#pokemonTable tbody').append(`
                                        <tr>
                                            <td>${name}</td>
                                            <td>${power}</td>
                                            <td>${rarity}</td>
                                            <td>${type}</td>
                                            <td>${height}</td>
                                            <td>${weight}</td>
                                            <td>${abilities}</td>
                                            <td>${forms}</td>
                                            <td>${baseExperience}</td>
                                        </tr>
                                    `);
                                },
                                error: function (error) {
                                    console.error('Error fetching Pokémon details:', error);
                                },
                            });
                        });
                    },
                    error: function (error) {
                        console.error('Error fetching Pokémon data:', error);
                    },
                });
            }

            // Initial load of Pokémon data
            fetchPokemon(offset);

            // Function to handle pagination
            function updatePaginationButtons() {
                $('#prevPage').prop('disabled', offset === 0);
                // Assuming you want to load all Pokémon data, you can remove the next page check.
                $('#nextPage').prop('disabled', false);
            }

            // Pagination: Load the previous page
            $('#prevPage').click(function () {
                offset -= pageSize;
                if (offset < 0) {
                    offset = 0;
                }
                fetchPokemon(offset);
                updatePaginationButtons();
            });

            // Pagination: Load the next page
            $('#nextPage').click(function () {
                offset += pageSize;
                fetchPokemon(offset);
                updatePaginationButtons();
            });

            // Initial pagination button state
            updatePaginationButtons();
        });
    </script>
</body>
</html>


