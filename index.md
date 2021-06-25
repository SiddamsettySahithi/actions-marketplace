<html lang="en">
    <head>
        <script type="text/javascript">
            var jsonFileToUrl = 'actions-data-url.txt';
            var jsonUrl = 'actions-data.json';

            function loadFile(url, isJson, callback) {
                var xobj = new XMLHttpRequest();                
                if (isJson) {
                    xobj.overrideMimeType("application/json");                    
                }

                xobj.open('GET', url, true);
                xobj.onreadystatechange = function () {
                    if (xobj.readyState == 4 && xobj.status == "200") {
                        // Required use of an anonymous callback as .open will NOT return a value but simply returns undefined in asynchronous mode
                        callback(xobj.responseText);
                    }
                };
                xobj.send(null);  
            }

            function init() {
                loadFile(jsonFileToUrl, false, function(response) {
                    console.log('found file with content' + response);
                    var jsonFileToUrl = response;

                    loadFile(jsonFileToUrl, true, function(response) {
                        var json = JSON.parse(response);

                        for(var index in json.actions) {
                            var action = json.actions[index];
                            document.getElementById('main').innerHTML += '<div class="panel">' + action.repoName + '</div><br />';
                        }
                    }
                    )}
                )};
                
            
        </script>

        <style>
            #main {
                border: solid 1px blue;
            }

            .panel {
                border: solid 1px orange;
            }
        </style>
    </head>

    <body onload="init()">
        <div id="main">

        </div>
    </body>
</html>