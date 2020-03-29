
# **Arduino @ Google Summer of Code 2020 Proposal**

## **Project: Write Examples For Official Libraries**
**Name:**  *Manthan Admane*

**GitHub Username:** *MisterAwesome23*

**GithubIssueTracker:** https://github.com/arduino/summer-of-code/issues/110

**Email:** admanemanthan23@gmail.com

**Skype Name:** live:admanemanthan23

**Time zone:**  India (GMT+5:30)



---

### Abstract

Right from beginner to all time pros, everyone starts a new project implementation with an idea in mind primarily and the intense drive to code secondly. To make this task of coding easier, every official library (even unofficial ones should) contains examples- leveraging basic syntax and functionality. Basically, they are a basic code collection that makes it easy for the user to connect and to test a sensor, display, module, or any hardware (or even software service functionality) and focus on the "idea" instead. This project aims at adding adding and improving appropriate examples to existing official libraries.

### Technical Details

Based on discussions with authorities in charge of this project- 
The project aims to acquire quality over quantity.
The project, in my opinion,  should aim to address "FOUR" libraries completely than aiming more with lower efficiency.

As of today, Arduino has 90 official libraries many of which many need improvements especially in the examples section- the section which is very useful for beginners and are also the stepping stone of any new project.

To instantiate my research rather than manually going through each each library I wrote a simple python script to get names of all repositories:
```python
import requests
import json

url = "https://api.github.com/orgs/arduino-libraries/repos?per_page=100"
payload = ""
headers = {
    'cache-control': "no-cache",
    'Postman-Token': "2955dab5-a5f5-407e-a5c8-7533464393c9"
    }
response = requests.request("GET", url, data=payload, headers=headers)

todos = json.loads(response.text)
loopEnd = len(todos)  

i = 0
while i < loopEnd:
  print(todos[i]["name"])
  i += 1
```
 

This prints out all the repositories.

Furthermore, I used the [Google Sheets Api](https://developers.google.com/sheets/api) to formulate the following sheet automatically (kindly refer to the link)-

https://docs.google.com/spreadsheets/d/1LOpYnRRaj5A0UoGtOMZDg1WZ_abkdnXNdqQl3q_zyTI/edit?usp=sharing

Here I have mentioned all the libraries with the number of examples each have.

 - The ones with zero are marked absent. 
 - Ones having six or more relevant examples are marked sufficient
 - Others are marked accordingly.

This will help me and mentors to funnel down to which exact libraries to focus on.

Also, the issues column indicate the issue I think is relevant to me. Relevant in terms of what I can and am willing to work right now. The issue column also contain any relevant piece of resource/comment which could be of help to the library. 

Also, I aim on covering all 90 libraries having a fair idea of all the standard protocols each library should abide by before selecting the four (approximate number) libraries to be aimed under this project.

Moreover, in case the the project demands to work on an unofficial library as well, I'd be more than willing to research more on this and suggest a few interesting ones like  [boltiot-arduino-helper](https://github.com/Inventrom/boltiot-arduino-helper), though this should not be a priority in my opinion.


### Illustration of writing example for an official library
With the COVID-19 lock-downs, I am in my hometown with minimum physical hardware available hands on hence this simple illustration was chosen. For the actual project implementation the complexity of the example can certainly be advanced which will decided upon discussions with the assigned mentor.

[Note: This is just a demo example just to portray the methodologies that can be used in implementing actual project examples to official library]

#### **Demo Example Name:** SimpleSiren

Description (added as SimpleSiren.txt): Haven't we all used horns / sirens. Just a touch on switch and siren blows. Just a tap back and its stops honking. This library provides just this. A bare minimum framework simulating a siren functioning.

Components needed (added to SimpleSiren.ino header comments): Arduino board (UNO used to demonstrate), Push button switch, 10k Ohm Resistor, 220 Ohm Resistor, Buzzer.

Appropriate place to be added: 
https://github.com/arduino/Arduino/tree/master/build/shared/examples/02.Digital/SimpleSiren

Layout (added as layout.png): An image showing how connections have to be made. This layout was created using [Fritzing](https://fritzing.org/home/). 

![Layout.png](https://drive.google.com/file/d/1NOqEI5awx0pS5KBmi1cFsqaoITD3Kt0X/view?usp=sharing)

Link to Layout.png- 
https://drive.google.com/file/d/1NOqEI5awx0pS5KBmi1cFsqaoITD3Kt0X/view?usp=sharing

Schematic (added as schematic.png):  An image showing the schematic diagram of an UNO with SimpleSiren setup.
![Schematic.png](https://drive.google.com/file/d/141HdATR8_6ggbrRTScs8v9CQuTajhFSN/view?usp=sharing)

Link to Scehmatic.png- 
https://drive.google.com/file/d/141HdATR8_6ggbrRTScs8v9CQuTajhFSN/view?usp=sharing

Code (saved as SimpleSiren.ino):
```Arduino
/*
  SimpleSiren

  Description:
  Haven't we all used horns / sirens. Just a touch on switch and siren blows.
  Just a tap back and its stops honking. This library provides just this.
  A bare minimum framework simulating a siren functioning.  

  A buzzer which is connected to digital pin 13 is blown,
  when pressing a pushbutton attached to pin 2.

  The circuit:
  - Buzzer attached from pin 13 to ground
  - pushbutton attached to pin 2 from +5V
  - 10K resistor attached to pin 2 from ground

  - Note: on most Arduinos do NOT come with a Buzzer on the board
    hence has to be attached to pin 13.

  created March 2020,
  by Manthan Admane
  
*/

// constants won't change. They're used here to set pin numbers:
const int buttonPin = 2;     // the number of the pushbutton pin
const int buzzerPin =  13;      // the number of the Buzzer pin

// variables will change:
int buttonState = 0;         // variable for reading the pushbutton status

void setup() {
  // initialize the Buzzer pin as an output:
  pinMode(buzzerPin, OUTPUT);
  // initialize the pushbutton pin as an input:
  pinMode(buttonPin, INPUT);
}

void loop() {
  // read the state of the pushbutton value:
  buttonState = digitalRead(buttonPin);

  // check if the pushbutton is pressed. If it is, the buttonState is HIGH:
  if (buttonState == HIGH) {
    // turn Buzzer on:
    digitalWrite(buzzerPin, HIGH);
  } else {
    // turn Buzzer off:
    digitalWrite(buzzerPin, LOW);
  }
}
```

As a demonstration of familiarity with git and GitHub, I've created a pull request with the above mentioned additions on official Arduino repository-
Link to pull: https://github.com/arduino/Arduino/pull/9920

The same code has been uploaded to Arduino Project Hub with compliance to all contributing and content guidelines demonstrating the understanding and importance Project Hub. Link-
https://create.arduino.cc/projecthub/misterawesome23/simplesiren-de8f43?ref=user&ref_id=1506630&offset=0


### Illustration of intermediate / advanced example for an official library [ArduinoGraphics]

I also understand that the project not only needs basic examples but also require the technical competency to form intermediate and and advanced level codes / examples. To demonstrate this, I have used [ArduinoGraphics](https://github.com/arduino-libraries/ArduinoGraphics) (which has zero examples currently)  to formulate an intermediate / advanced example.

ArduinoGraphics is a Core graphics library for Arduino based on the Processing API. For now it does not have any example which can run on the Arduino serial monitor. It needs an external screen along with its specific hardware interface library to drive the screen but it's graphical primitives can certainly be leveraged without one.

Special thanks to [Prcoessing]([[https://processing.org/](https://processing.org/)) for the Hello Processing tutorial to introduce to processing, the syntax on which ArduinoGraphics library is heavily based on. Also, [adafruit-gfx-graphics-library]([https://learn.adafruit.com/adafruit-gfx-graphics-library/graphics-primitives](https://learn.adafruit.com/adafruit-gfx-graphics-library/graphics-primitives)) provided a good reference. Finally, thanks to one of our community member **per1234** (gitHubHandle) for helping me with this example for providing resources for formulating the initial code framework. 

Code- (MarqueeGSoC.ino)

```Arduino
/*
  Use this library for testing and drawing ASCII art and testingSerial monitor.
  See the https://www.arduino.cc/en/Reference/ArduinoGraphics and
  https://github.com/arduino-libraries/Arduino_MKRRGB for a more
  useful demonstration of the ArduinoGraphics library.
  Code samples in the reference are released into the public domain.
*/

// Include ArduinoGraphics library from Sketch -> Include library
// or download and https://github.com/arduino-libraries/ArduinoGraphics add zip
#include <ArduinoGraphics.h>


// Initalise canvas
const byte canvasWidth = 61;
const byte canvasHeight = 27;


// Make ASCIIDrawClass class whose object can access ArduinoGraphics functions
class ASCIIDrawClass : public ArduinoGraphics {
  public:
    // can be used with an object of any class that inherits from the Print class
    ASCIIDrawClass(Print &printObject = (Print &)Serial) :
      ArduinoGraphics(canvasWidth, canvasHeight),
      _printObject(&printObject) {}

    // this function is called by the ArduinoGraphics library's functions
    virtual void set(int x, int y, uint8_t r, uint8_t g, uint8_t b) {
      // the r parameter is (mis)used to set the character to draw with
      _canvasBuffer[x][y] = r;
      // cast unused parameters to void to fix "unused parameter" warning
      (void)g;
      (void)b;
    }

    // display the drawing on Serial Monitor
    void endDraw() {
      ArduinoGraphics::endDraw();

      for (byte row = 0; row < canvasHeight; row++) {
        for (byte column = 0; column < canvasWidth; column++) {
          // handle unset parts of buffer
          if (_canvasBuffer[column][row] == 0) {
            _canvasBuffer[column][row] = ' ';
          }
          _printObject->print(_canvasBuffer[column][row]);
        }
        _printObject->println();
      }
    }

  private:
    Print *_printObject;
    char _canvasBuffer[canvasWidth][canvasHeight] = {{0}};
};

// Create object to access functions
// Note ASCII draw to be replaced by "YourScreen"
ASCIIDrawClass ASCIIDraw;

void setup() {
  Serial.begin(9600);
  while (!Serial);

  ASCIIDraw.beginDraw();

  // configure the character used to fill the background. The second and third parameters are ignored
  ASCIIDraw.background('+', 0, 0);
  ASCIIDraw.clear();

  // add the text
  ASCIIDraw.background(' ', 0, 0);
  ASCIIDraw.stroke('#', 0, 0);
  const char text[] = "GSOC";

  // Two options Font_5x7 or Font_4x6 
  ASCIIDraw.textFont(Font_5x7);
  const byte textWidth = strlen(text) * ASCIIDraw.textFontWidth();
  const byte textHeight = ASCIIDraw.textFontHeight();
  const byte textX = (canvasWidth - textWidth) / 4;
  const byte textY = (canvasHeight - textHeight) / 4;
  ASCIIDraw.text(text, textX, textY);

  // add scrolling / marcquee text
  ASCIIDraw.background('-', 0, 0);
  ASCIIDraw.beginText(40, 0, '#', 0, 0);
  ASCIIDraw.textScrollSpeed(100);
  ASCIIDraw.print("HEY");
  ASCIIDraw.endText(true);


  // print the drawing to the Serial Monitor
  ASCIIDraw.endDraw();
}

void loop() {}
```

Also, the code above written code follows all coding and contribution guidelines for Ardiuno and code formatting is consistent with the style used in the existing code for ArduinoGraphics.

**Working Screenshots and Video:**

![MarqueeSSOne](https://drive.google.com/file/d/1Jr-jgKS3UAP4toeBPB62DZe82wHTjUQ7/view?usp=sharing)
Link- https://is.gd/MarqueeSSOne


![MarqueeSSTwo](https://drive.google.com/file/d/1OscYqhyG_Sh095Q83XQ9Z6kRHUaMCLaM/view?usp=sharing)
Link- https://is.gd/MarqueeSSTwo

Video Link- https://is.gd/ArduinoGraphicsGSoCExamplVideo

### **Basic characteristic of a good example-**
Link to diagram for this- https://is.gd/basicExampleCharacteristics
1. **Overall Quality:**  
Readable, well indented code complying to standard coding style. Overall well defined structure.
2. **Well commented:**  
A code with appropriate commenting indicating flow and explaining why and what in brief.
3. **Creativity:**  
Should be intriguing and practical at the same time. Easier association to real life examples are easier to  follow.
4. **Boilerplate:**  
Examples should work as boilerplate codes to extend application to other projects.
5. **Expected Output:**  
It should be provided with the examples to ensure proper functioning of the device and configurations on  a basic or initial level.
6. **Larger syntax  coverage:**  
For intermediate and advanced examples a larger functionality and  syntax coverage is desirable.




### Contributions
1. https://github.com/arduino-libraries/ArduinoSound/pull/24
2.  https://github.com/arduino-libraries/Ciao/pull/6
3. https://github.com/arduino-libraries/USBHost/issues/14
4. https://github.com/arduino-libraries/AudioFrequencyMeter/issues/15
5. https://github.com/arduino-libraries/ArduinoGraphics/pull/14#pullrequestreview-382503771
6. https://forum.arduino.cc/index.php?topic=673524.0
7. https://github.com/arduino-libraries/Arduino_CRC32/pull/6
8. https://github.com/arduino-libraries/NTPClient/issues/92
9. https://github.com/arduino-libraries/NTPClient/issues/91
10. https://github.com/arduino-libraries/NTPClient/issues/89 
11. https://github.com/arduino-libraries/NTPClient/issues/87



### Schedule of Deliverables




#### **Application Review Period (March 31, 2020 - April 30, 2020)**
- Cover all 90 repositories under arduino-official libraries.
- Fix issues and create necessary pull-requests.
- Finalize on ten (approximate number) which I feel are most relevant to this project and align with my interests.


#### **Community Bonding Period (May 4, 2020 - May 31, 2020)**

	

 1. Get familiar with the Style-guide and contribution guidelines for the Arduino community.
 2. Discuss and finalize plan or timeline with my mentor.
 3. Plan platform of communication for weekly calls/meetings, to submit my weekly report to the mentor (also finalize on report formats- Example: A [GitHub blog](https://github.blog/)).
 4. Plan my work time-table for summer.
 5. Most importantly, get innately involved in the community like a family member :)

#### **Phase 1 (June 1, 2020 - July 3, 2020)**

* Deliverable 1
	* Week 1- **Library One** resource collection and familiarization. Draft examples and implementation.
	* Week 2- Finalize the example and fix problems for example along with a projectHub submission of the library.
* Deliverable 2
	* Week 3- **Library Two** working. Adjust working hours and styles with reference to Library One. Change buffer time and methodologies.
	* Week 4- Fix problems in the added examples and work on prototype examples.


#### **Phase 2 (July 4, 2020 - July 31, 2020)**

* Deliverable 3
	* Week 5- **Library Three** resource collection and familiarization. Focus on improving the efficiency of work from Week 1-4 learning's.
	* Week 6- Fix bugs and issues suggested by mentor and community. Proceed to projectHub possibilities.
* Deliverable 4
	* Week 7- **Library FOUR** resource collection and familiarization. Create examples and draft formal implementation diagrams for the respective example.
	* Week 8- Fix issues with newly added example and build a basic hardware prototype displaying the usage of added example.

#### **Phase 3 (August 1, 2020 - August 23, 2020)**

* Deliverable 5
	* Week 9- Develop advanced examples for one of the above utilized four libraries.
	* Week 10- Test and improve the advanced example to improve on code readability and easier to understand though conveying a complex application.
* Deliverable 6
	* Week 11- Fix bugs and issues previous implementation and implement an advanced example project further publishing it to Project Hub.


#### **Final Week (August 24, 2020 - August 31, 2020)**

* Deliverable 8
	* Week 12- Finalize on all the documentations. Fix upcoming bugs and proof-read all implementations. Rather than focusing on adding more, the focus will be on consolidating what already has been implemented in the project.

### Development Experience

One ongoing final year project (IoT + Data Science) and one completed project (Android app) both implemented remotely in team of four members via GitHub portraying familiarity with git.
	
  1. https://github.com/SDLMiniProject/PPMS
  2. https://github.com/BE-Project-cl-AIR-ity/clairity
  

Past project implementation and understanding with techniques like [Pomodoro](https://en.wikipedia.org/wiki/Pomodoro_Technique) and [Timeboxing]( https://en.wikipedia.org/wiki/Timeboxing) gives me an efficiency advantage.

### Other Experiences
Using GitHub API and GoogleSheets API for this very project to portraying my abilities to focus on efficiency of work.

University certified course on Internet of Things.

Wifi deauther under learning ethical hacking- 
https://github.com/MisterAwesome23/esp8266_deauther 

Resume: 
https://is.gd/ManthanArduinoGSoCResume


### Why this project?


I have been applying to GSoC for past two years (not selected). One thing I've learned is- its all about Open Source Contributions and being a selfless contributor majorly. Self learning and everything else are just supplementary positive add-ons. I personally have know Arduino since my childhood and I would choose contributing to something I consume than to work for something I have no direct co-relations to. This year I will be applying to one organisation and one project only- Write Examples For Official Libraries. I want to keep my area of work as niche as possible and contribute as much as I can no matter how small or big. Also, even if I do not get selected for GSoC2020 (which I really want be selected for) I'll continue with Arduino as my organisation and start for Google Summer of Docs 2020 abiding by my want to be innately connected to an open source community.

### Do you have any other commitments during the GSoC period?


- I will be having my university practical examinations for two days and university final year written examinations (four exams). Because of the ongoing COVID-19 pandemic the dates are not consolidated.
- I will be starting my Masters in Management Information System Fall 2020 at Texas A&M. Dates not announced.


