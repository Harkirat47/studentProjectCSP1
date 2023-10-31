---
toc: True
comments: False
layout: post
title: Javascript todo list
type: hacks
courses: {'csp': {'week': 3}}
---

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <script>
        window.onload = () => {
            const form1 = document.querySelector("#addForm");

            let items = document.getElementById("items");
            let submit = document.getElementById("submit");

            let editItem = null;

            form1.addEventListener("submit", addItem);
            items.addEventListener("click", removeItem);
        };

        function addItem(e) {
            e.preventDefault();

            if (submit.value != "Submit") {
                console.log("Hello");

                editItem.target.parentNode.childNodes[0].data
                    = document.getElementById("item").value;

                submit.value = "Submit";
                document.getElementById("item").value = "";

                document.getElementById("lblsuccess").innerHTML
                    = "Text edited successfully";

                document.getElementById("lblsuccess")
                    .style.display = "block";

                setTimeout(function () {
                    document.getElementById("lblsuccess")
                        .style.display = "none";
                }, 3000);

                return false;
            }

            let newItem = document.getElementById("item").value;
            if (newItem.trim() == "" || newItem.trim() == null)
                return false;
            else
                document.getElementById("item").value = "";

            let li = document.createElement("li");
            li.className = "list-group-item";

            let deleteButton = document.createElement("button");

            deleteButton.className =
                "btn-danger btn btn-sm float-right delete";

            deleteButton.appendChild(document.createTextNode("Delete"));

            let editButton = document.createElement("button");

            editButton.className =
                "btn-success btn btn-sm float-right edit";

            editButton.appendChild(document.createTextNode("Edit"));

            li.appendChild(document.createTextNode(newItem));
            li.appendChild(deleteButton);
            li.appendChild(editButton);

            items.appendChild(li);
        }

        function removeItem(e) {
            e.preventDefault();
            if (e.target.classList.contains("delete")) {
                if (confirm("Are you Sure?")) {
                    let li = e.target.parentNode;
                    items.removeChild(li);
                    document.getElementById("lblsuccess").innerHTML
                        = "Text deleted successfully";

                    document.getElementById("lblsuccess")
                        .style.display = "block";

                    setTimeout(function () {
                        document.getElementById("lblsuccess")
                            .style.display = "none";
                    }, 3000);
                }
            }
            if (e.target.classList.contains("edit")) {
                document.getElementById("item").value =
                    e.target.parentNode.childNodes[0].data;
                submit.value = "Finish";
                editItem = e;
            }
        }

        function toggleButton(ref, btnID) {
            document.getElementById(btnID).disabled = false;
        }
    </script>

    <title>To Do List</title>
</head>

<body>

    <div class="container mt-3">
        <p>Add Items</p>

        <label id="lblsuccess" class="text-success" style="display: none;">
        </label>

        <form id="addForm">
            <div class="row">
                <div class="col-lg-7 col-md-7 col-sm-7">

                    <input type="text" onkeyup="toggleButton(this, 'submit')" class="form-control" id="item">
                </div>

                <div class="col-lg-5 col-md-5 col-sm-5">
                    <input type="submit" class="btn btn-dark" id="submit" value="Submit" disabled>
                </div>
            </div>
        </form>

        <p>Tasks</p>

        <form id="addForm">
            <ul class="list-group" id="items"></ul>
        </form>
    </div>
</body>

<hr style="solid">

### The Code


```python
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">

    <link rel="stylesheet" href="https://stackpath.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css"
        integrity="sha384-ggOyR0iXCbMQv3Xipma34MD+dH/1fQ784/j6cY/iJTQUOhcWr7x9JvoRxT2MZw1T" crossorigin="anonymous">

    <script>
        // loading the form
        window.onload = () => { 
            const form1 = document.querySelector("#addForm");

            let items = document.getElementById("items");
            let submit = document.getElementById("submit");

            let editItem = null;

            form1.addEventListener("submit", addItem); // buttons
            items.addEventListener("click", removeItem);
        };

        function addItem(e) {
            e.preventDefault();

            if (submit.value != "Submit") { //editing as well as submit
                console.log("Hello");

                editItem.target.parentNode.childNodes[0].data
                    = document.getElementById("item").value;

                submit.value = "Submit";
                document.getElementById("item").value = "";

                document.getElementById("lblsuccess").innerHTML
                    = "Text edited successfully";

                document.getElementById("lblsuccess")
                    .style.display = "block";

                setTimeout(function () {
                    document.getElementById("lblsuccess")
                        .style.display = "none";
                }, 3000);

                return false;
            }

            let newItem = document.getElementById("item").value;
            if (newItem.trim() == "" || newItem.trim() == null)
                return false;
            else
                document.getElementById("item").value = "";

            let li = document.createElement("li");
            li.className = "list-group-item";

            let deleteButton = document.createElement("button");

            deleteButton.className =
                "btn-danger btn btn-sm float-right delete"; //delete button

            deleteButton.appendChild(document.createTextNode("Delete"));

            let editButton = document.createElement("button");

            editButton.className =
                "btn-success btn btn-sm float-right edit"; //edit button

            editButton.appendChild(document.createTextNode("Edit"));

            li.appendChild(document.createTextNode(newItem));
            li.appendChild(deleteButton);
            li.appendChild(editButton);

            items.appendChild(li);
        }

        function removeItem(e) {
            e.preventDefault();
            if (e.target.classList.contains("delete")) {
                if (confirm("Are you Sure?")) { //delete confirmation
                    let li = e.target.parentNode;
                    items.removeChild(li);
                    document.getElementById("lblsuccess").innerHTML
                        = "Text deleted successfully";

                    document.getElementById("lblsuccess")
                        .style.display = "block";

                    setTimeout(function () {
                        document.getElementById("lblsuccess")
                            .style.display = "none";
                    }, 3000);
                }
            }
            if (e.target.classList.contains("edit")) {
                document.getElementById("item").value =
                    e.target.parentNode.childNodes[0].data;
                submit.value = "Finish";
                editItem = e;
            }
        }

        function toggleButton(ref, btnID) {
            document.getElementById(btnID).disabled = false;
        }
    </script>

    <title>To Do List</title>
</head>

<body>
    <!-- the pretty gui stuff -->

    <div class="container mt-3">
        <p>Add Items</p>

        <label id="lblsuccess" class="text-success" style="display: none;">
        </label>

        <form id="addForm">
            <div class="row">
                <div class="col-lg-7 col-md-7 col-sm-7">

                    <input type="text" onkeyup="toggleButton(this, 'submit')" class="form-control" id="item">
                </div>

                <div class="col-lg-5 col-md-5 col-sm-5">
                    <input type="submit" class="btn btn-dark" id="submit" value="Submit" disabled>
                </div>
            </div>
        </form>

        <p>Tasks</p>

        <form id="addForm">
            <ul class="list-group" id="items"></ul>
        </form>
    </div>
</body>
```