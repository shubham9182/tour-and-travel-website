
<html>
<head>
		  <link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/css/bootstrap.min.css">
  <script src="https://ajax.googleapis.com/ajax/libs/jquery/3.4.1/jquery.min.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/popper.js/1.14.7/umd/popper.min.js"></script>
  <script src="https://maxcdn.bootstrapcdn.com/bootstrap/4.3.1/js/bootstrap.min.js"></script>
<link rel="stylesheet" href="https://cdnjs.cloudflare.com/ajax/libs/font-awesome/4.7.0/css/font-awesome.min.css">
    <script type="text/javascript" >// <![CDATA[ 
        function loading(){
            $("#loading").show();
            $("#content").hide();       
        }
// ]]></script>
	<title>Alexa</title>
	
	<style>
		
    
 .heading { color: hsl(0, 0%, 3%);}  

.page th {
    background-color: #add8e6;
    color: rgb(51, 21, 21);
}
body {

  
	
  background-image: url("https://th.bing.com/th/id/R.23d210484ee2e67880b826cd414b8edd?rik=Nu41w%2brrPCUyoA&riu=http%3a%2f%2fpavbca.com%2fwalldb%2foriginal%2fd%2ff%2f4%2f482983.jpg&ehk=LHSLM1PxYrrtYbrmdhLvvR67%2bak%2bySUmcgRmFhR6Otg%3d&risl=&pid=ImgRaw&r=0");
  background-color: #cccccc;
  height: 755px;
  background-position: center;
  background-repeat: no-repeat;
  background-size: cover;
  position: relative;
    
   
}
div#loading {
 
    width: 1700px;
    height: 35px;
    display: none;
    background: url('{{ url_for('static', filename='loading_bar.gif' ) }}') no-repeat;
    cursor: wait;
    
  }
  
.center {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 30px;}

.center1 {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 5px;
}


</style>
</head>
<body>
 <div>
	<h1 class="heading center"> </h1>
	<h1 class="heading center"> </h1>
	<form method="POST" action="/" enctype="multipart/form-data">	
	 <button type="submit" class="btn btn-primary button_add" style="margin: 0 auto;display: block; border-radius: 12px;width:100px;"><i class="fa fa-microphone"></i></button>
   <h1 class="heading center1">TAP TO SPEAK</h1>
   	</form>
	<form method="GET" action="/" enctype="multipart/form-data">
	</form>
	<br>
	<div id="loading" ><br>
  <p class="heading"> Please wait </p></div>
<br>
</div>

</body>
</html>
from flask import Flask, render_template, redirect, request
import warnings

warnings.filterwarnings('ignore')

import speech_recognition as sr
import pyttsx3
import pywhatkit
import datetime
import pyjokes
import wikipedia
import sys
import requests, json

listener = sr.Recognizer()
# engine = pyttsx3.init()

import os

app = Flask("__name__")


def engine_talk(text):
    engine = pyttsx3.init()
    voices = engine.getProperty("voices")
    engine.setProperty('voice', voices[1].id)
    engine.say(text)
    engine.runAndWait()


def user_commands():
    try:
        with sr.Microphone() as source:
            print("Start Speaking!!")
            voice = listener.listen(source)
            command = listener.recognize_google(voice)
            command = command.lower()
            command = command.replace('alexa', '')
            if 'alexa' in command:
                print(command)
    except:
        pass
    return command


def weather(city):
    # Enter your API key here
    api_key = "<YOUR API KEY>"
    # How to use api_key, see the below code:
    # api_key = "ABCDE"

    # base_url variable to store url
    base_url = "http://api.openweathermap.org/data/2.5/weather?"

    # Give city name
    city_name = city

    # complete_url variable to store
    # complete url address
    complete_url = base_url + "appid=" + api_key + "&q=" + city_name

    # get method of requests module
    # return response object
    response = requests.get(complete_url)

    # json method of response object
    # convert json format data into
    # python format data
    x = response.json()

    # Now x contains list of nested dictionaries
    # Check the value of "cod" key is equal to
    # "404", means city is found otherwise,
    # city is not found
    if x["cod"] != "404":
        # store the value of "main"
        # key in variable y
        y = x["main"]

        # store the value corresponding
        # to the "temp" key of y
        current_temperature = y["temp"]
        temp_in_celcius = current_temperature - 273.15
        return str(int(temp_in_celcius))


def run_alexa():
    command = user_commands()
    if 'play a song' in command:
        song = 'Arijit Singh'
        engine_talk('Playing some music')
        print("Playing....")
        pywhatkit.playonyt(song)
    elif 'play' in command:
        song = command.replace('play', '')
        engine_talk('Playing....' + song)
        print("Playing....")
        pywhatkit.playonyt(song)
    elif 'time' in command:
        time = datetime.datetime.now().strftime('%I:%M %p')
        print(time)
        engine_talk('Current Time is' + time)
    elif 'joke' in command:
        get_j = pyjokes.get_joke()
        print(get_j)
        engine_talk(get_j)
    elif 'who is' in command:
        person = command.replace('who is', '')
        info = wikipedia.summary(person, 1)
        print(info)
        engine_talk(info)
    elif 'weather' in command:
        # engine_talk('Please tell name of the city')
        city = 'Hong Kong'
        # city = 'Mumbai'
        engine_talk('The temperature in Hong Kong is' + weather(city) + 'degree celcius')
    elif 'stop' in command:
        engine_talk("Good bye")
    else:
        engine_talk("I didn't hear you properly")
        print("I didn't hear you properly")


@app.route('/')
def hello():
    return render_template("shubham.html")


@app.route("/home")
def home():
    return redirect('/')


@app.route('/', methods=['POST', 'GET'])
def submit():
    while True:
        run_alexa()
    return render_template("shubham.html")


if __name__ == "__main__":
    app.run(debug=True)
