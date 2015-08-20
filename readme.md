# New & Improved Arduino Button Library

The Arduino Button library makes it easy to do some very common but rather 
tedious tasks, including detecting clicks, long presses, and debouncing.

Usually when you interact with a button (such as a momentary 
switch), you mainly want to detect the state change, not just the current 
state.  You have to do something like:

	int lastState = 0;

	void loop(){
		int currentState = digitalRead(11);
		if(currentState != lastState){
			// do something
		}
		lastState = currentState;
	}

It's not hard, just tedious.  This new and improved Button library makes this 
much simpler but adds so much more.  Now you can do it this way:

	Button button = Button(12);

	void onPress(Button& b){
		Serial.print("onPress: ");
		Serial.println(b.pin);
		// will print out "onPress: 12"
	}

	void setup(){
	  Serial.begin(9600);
	  // Assign callback function
	  button.pressHandler(onPress);
	}

	void loop(){
	  // update the buttons' internals
	  button.process();
	}

## Features

* Instance-based design

	`Button myButton(11);`

* Automatic pull-up setting

	`Button myButton(11, BUTTON_PULLUP_INTERNAL);`

* Simplified state-change detection:

	`if(button.isPressed()) ...` isPressed() accounts for debouncing,
	so you don't have to worry about false presses.

* Callback model

	`button.pressHandler(onPress)`

	There are 4 callbacks you can (optionally) use: press, release,
	click, and hold. 'press' and 'release' are sent for every button.
	'click' and 'hold' are exclusive. 

	- 'hold' will be sent for a long press, before 'release'
	- 'click' will be sent for a short press, after 'release'

* Built-in debouncing

    `// Sets 50ms debounce duration`

    `Button button = Button(12, BUTTON_PULLUP_INTERNAL, true, 50);`

## Installing

## Credits

 By Ted Hayes, from code originally by Alexander Brevig & Tom Igoe. 
 Additionally modified by Lee Thomason.

