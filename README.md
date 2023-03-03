# DeeonStjean.github.io
<!doctype html>
<html lang="en">
<head>
	<!-- Required meta tags -->
	<meta charset="utf-8">
	<meta name="viewport" content="width=device-width, initial-scale=1">

	<!-- Bootstrap CSS -->
	<link href="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css" rel="stylesheet" integrity="sha384-1BmE4kWBq78iYhFldvKuhfTAU6auU8tT94WrHftjDbrCEXSU1oBoqyl2QvZ6jIW3" crossorigin="anonymous">
	<style>
        body {
            background-image: url(https://img.freepik.com/free-photo/cloud-sky-twilight-times_74190-4017.jpg)
        }
        ul li {
            cursor: pointer;
            position: relative;
            padding: 6px 10px 6px 30px;
            font-size: 18px;
            transition: 0.2s;
            /* make the list items unselectable */
            -webkit-user-select: none;
            -moz-user-select: none;
            -ms-user-select: none;
            user-select: none;
        }
        ul li.checked {
            text-decoration: line-through;
        }
        ul li.checked::before {
            content: '';
            position: absolute;
            border-color: #fff;
            border-style: solid;
            border-width: 0 2px 2px 0;
            top: 10px;
            left: 16px;
            transform: rotate(45deg);
            height: 15px;
            width: 7px;
        }
        h1 {
            color: black;
            text-align: center;
        }
        td {
            padding: 5px;
        }
        .strike {
            text-decoration: line-through;
        }
    </style>
       

	<title>Hello, World!</title>
</head>
<body>
    <h1>To Do List!</h1>
    <!-- Optional JavaScript; choose one of the two! -->
    <audio id= "sound1" src="https://interactive-examples.mdn.mozilla.net/media/cc0-audio/t-rex-roar.mp3"></audio>

    <input type="text" placeholder="Add to the list">
    <p>
        date:
        <input type="date" id="dateInput">
    </p>
    <p>
        <label> Select your color</label>
        <input type="color" id="colorInput" name="color">
    </p>
    <button id="addBtn">Add</button>
    <ul id="myUL">
        <li>Hit the gym</li>
        <li>Pay bills</li>
        <li>Pick up mom from airport</li>
        <li>Buy eggs</li>
        <li>Read a book</li>
        <li>Clean my room</li>
        <li>Do laundry</li>
    </ul>


    <!-- Option 1: Bootstrap Bundle with Popper -->
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.bundle.min.js" integrity="sha384-ka7Sk0Gln4gmtz2MlQnikT1wXgYsOg+OMhuP+IlRH9sENBO0LRn5q+8nbTov4+1p" crossorigin="anonymous"></script>

    <!-- Option 2: Separate Popper and Bootstrap JS -->
    <!--
    <script src="https://cdn.jsdelivr.net/npm/@popperjs/core@2.10.2/dist/umd/popper.min.js" integrity="sha384-7+zCNj/IqJ95wo16oMtfsKbZ9ccEh31eOz1HGyDuCQ6wgnyJNSYdrPa03rtR1zdB" crossorigin="anonymous"></script>
    <script src="https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/js/bootstrap.min.js" integrity="sha384-QJHtvGhmr9XOIpI6YVutG+2QOK9T+ZnN4kzFN1RtK3zEFEIsxhlmWl5/YESvpZ13" crossorigin="anonymous"></script>
    -->
    <script>

        //to show the delete button
        var myNodelist = document.getElementsByTagName("LI");
        var i;
        for (i = 0; i < myNodelist.length; i++) {
            var span = document.createElement("SPAN");
            var txt = document.createTextNode("\u00D7");
            span.className = "close";
            span.appendChild(txt);
            myNodelist[i].appendChild(span);
        }
        // delete items from list
        var close = document.getElementsByClassName("close");
        var i;
        for (i = 0; i < close.length; i++) {
            close[i].onclick = function () {
                var div = this.parentElement;
                div.style.display = "none";
            }
        }
        //Add a sound when clicking on a list item
        var sound = document.querySelector('ul');
        sound.addListeners("click", play)
        function play() {
            var audio = document.getElementById("sound1");
            audio.play();
        }

        // Add a "checked" symbol when clicking on a list item
        var list = document.querySelector('ul');
        list.addEventListener('click', function (ev) {
            if (ev.target.tagName === 'LI') {
                ev.target.classList.toggle('checked');
            }
        }, false);
        onload = todoMain;

        function todoMain() {
            let inputElem,
                dateInput,
                colorInput,
                button,
                ulElem;

            getElements();
            addListeners();

            function getElements() {
                inputElem = document.getElementsByTagName("input")[0];
                dateInput = document.getElementById("dateInput");
                colorInput = document.getElementById("colorInput");
                button = document.getElementById("addBtn");
                ulElem = document.getElementsByTagName("ul")[0];
            }

            function addListeners() {
                button.addEventListener("click", addEntry, false);
            }

            function addEntry(event) {

                let inputValue = inputElem.value;
                inputElem.value = "";

                let dateValue = dateInput.value;
                dateInput.value = "";

                let colorValue = colorInput.value;
                colorInput.value = "";
                // add a new row

                let list = document.getElementById("myUL");

                let trElem = document.createElement("li");
                list.appendChild(trElem);

                // checkbox cell
                let checkboxElem = document.createElement("li");
                checkboxElem.type = "checkbox";
                checkboxElem.addEventListener("click", done, false);
                let tdElem1 = document.createElement("td");
                //tdElem1.appendChild(checkboxElem);
                //trElem.appendChild(tdElem1);

                // to-do cell
                let tdElem2 = document.createElement("td");
                tdElem2.innerText = inputValue;
                trElem.appendChild(tdElem2);

                //date cell
                let dateElem = document.createElement("td");
                dateElem.innerText = dateValue;
                trElem.appendChild(dateElem);

                //color cell
                let colorElem = document.createElement("td");
                colorElem.innerText = colorValue;
                trElem.appendChild(colorElem);

                // delete cell
                let spanElem = document.createElement("span");
                spanElem.innerText = "x";
                spanElem.className = "close";
                spanElem.addEventListener("click", deleteItem, false);
                let tdElem4 = document.createElement("td");
                tdElem4.appendChild(spanElem);
                trElem.appendChild(tdElem4);


                function deleteItem() {
                    trElem.remove();
                }

                function done() {
                    trElem.classList.toggle("strike");
                }

            }
        }
    </script>

</body>
</html>
