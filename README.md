# simpledartprogram
This program is an example of a simple quiz format for a dart program. 
import 'package:flutter/material.dart';
import 'package:flutter_login/flutter_login.dart';
import 'dashboard_screen.dart';

void main() => runApp(MyApp());


class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      home: MyInitialPage(),
    );
  }
}

class MyInitialPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: new Color(0x673AB7),
          title: Text('Music Preference Questionnaire'),
        ),
        body: Center(
            child: Column(
                mainAxisAlignment: MainAxisAlignment.center,
                children: <Widget>[
                  RaisedButton(child: Text('HELP')),
                  new RaisedButton(
                      child: Text("Continue to the Survey"),
                      onPressed: () {Navigator.of(context).push( MaterialPageRoute<Null>(builder: (BuildContext context) {
                        return new UserLogin();
                      }));
                      Padding(
                          padding: EdgeInsets.all(25.0)
                      );

                      new Row(children: <Widget>[
                      new RaisedButton(
                          child: Text("Admin Login"),
                          onPressed: () {Navigator.of(context).push(MaterialPageRoute<Null>(builder: (BuildContext context) {
                            return new UserLogin();
                          }));
                          })]);
                      })

                ])));
  }


  MyInitialPage();

}

class UserLogin extends StatefulWidget {
  @override
  _UserLoginState createState() => _UserLoginState();
}

const users = const {
  'dribbble@gmail.com': '12345',
  'hunter@gmail.com': 'hunter',
};

class LoginScreen extends StatelessWidget {
  Duration get loginTime => Duration(milliseconds: 2250);

  Future<String> _authUser(LoginData data) {
    print('Name: ${data.name}, Password: ${data.password}');
    return Future.delayed(loginTime).then((_) {
      if (!users.containsKey(data.name)) {
        return 'Username not exists';
      }
      if (users[data.name] != data.password) {
        return 'Password does not match';
      }
      return null;
    });
  }

  Future<String> _recoverPassword(String name) {
    print('Name: $name');
    return Future.delayed(loginTime).then((_) {
      if (!users.containsKey(name)) {
        return 'Username not exists';
      }
      return null;
    });
  }

  @override
  Widget build(BuildContext context) {
    return FlutterLogin(
      title: 'ECORP',
      logo: 'assets/images/ecorp-lightblue.png',
      onLogin: _authUser,
      onSignup: _authUser,
      onSubmitAnimationCompleted: () {
        Navigator.of(context).pushReplacement(MaterialPageRoute(
          builder: (context) => DashboardScreen(),
        ));
      },
      onRecoverPassword: _recoverPassword,
    );
  }
}


//homepage that takes the user to the questionnaire
class MyHomePage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: new Color(0x673AB7),
          title: Text('Music Preference Questionnaire'),
        ),
        body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text("Thank you for participating in this questionnaire"),
                Text("your answers are always appreciated!"),
                RaisedButton(child: Text("Click to begin"), onPressed: (){
                  Navigator.of(context) .push(MaterialPageRoute<Null>(builder: (BuildContext context ) {
                    return new MyQuestionnaire();
                  }));
                }
                )],
            )

        ));
  }

  MyHomePage();

}


class MyQuestionnaire extends StatefulWidget {
  MyQuestionnaire();


  @override
  _MyQuestionnaireState createState() => _MyQuestionnaireState();
}
const _classical = "Classical";
const _country = "Country";
const _classicRock = "Classic Rock";
const _christian = "Christian";
const _pop = "Pop";
const _heavyMetal = "Heavy Metal";
const _rap = "Rap/Hip Hop";
const _metal = "Metal" ;
const _alternative = "Alternative/Folk" ;
const _jazz = "Jazz";
const _blues = "Blues";

const _listOfGenres  = [
  DropdownMenuItem(value: _classical, child: Text(_classical)),
  DropdownMenuItem(value: _country, child: Text(_country)),
  DropdownMenuItem(value: _classicRock, child: Text(_classicRock)),
  DropdownMenuItem(value: _christian, child: Text(_christian)),
  DropdownMenuItem(value: _pop, child: Text(_pop)),
  DropdownMenuItem(value: _heavyMetal, child: Text(_heavyMetal)),
  DropdownMenuItem(value: _rap, child: Text(_rap)),
  DropdownMenuItem(value: _metal, child: Text(_metal)),
  DropdownMenuItem(value: _alternative, child: Text(_alternative)),
  DropdownMenuItem(value: _jazz, child: Text(_jazz)),
  DropdownMenuItem(value: _blues, child: Text(_blues)),


];

const _itunes = "iTunes";
const _apple = "Apple music" ;
const _spotify = "Spotify" ;
const _youtube = "Youtube" ;
const _radio = "Radio" ;

const _listOfMedium = [
  DropdownMenuItem(value: _itunes, child: Text(_itunes)),
  DropdownMenuItem(value: _apple, child: Text(_apple)),
  DropdownMenuItem(value: _spotify, child: Text(_spotify)),
  DropdownMenuItem(value: _youtube, child: Text(_youtube)),
  DropdownMenuItem(value: _radio, child: Text(_radio)),
];

const _temp = "Tempo/speed";
const _voice = "The singer's voice";
const _message = "The message of the song";
const _instrument = "The instruments being used";

const _listOfMusic = [
  DropdownMenuItem(value: _temp, child: Text(_temp)),
  DropdownMenuItem(value: _voice, child: Text(_voice)),
  DropdownMenuItem(
      value: _message, child: Text(_message)),
  DropdownMenuItem(
      value: _instrument , child: Text(_instrument)),
];


class _MyQuestionnaireState extends State<MyQuestionnaire> {
  int _genderValue = null;
  int _ageValue = null;
  var _genreValue;
  double _sliderValue = 0.0 ;
  var _mediumValue;
  var _musicAspect;
  bool _isPressed = false ;

  void _refreshGenderValue (int newValue){
    setState((){
      _genderValue = newValue ;
    });
  }

  void _refreshAgeValue (int newValue){
    setState((){
      _ageValue = newValue ;
    });
  }
  void _refreshGenreKindDropdown(String newValue) {
    setState(() => _genreValue = newValue);
  }

  void _refreshSlider(double newValue){
    setState((){
      _sliderValue = newValue;
    });
  }

  void _refreshMediumValueDropdown (String newValue) {
    setState(() => _mediumValue = newValue );
  }

  TextEditingController oneController = new TextEditingController();
  TextEditingController twoController = new TextEditingController();
  TextEditingController threeController = new TextEditingController();

  void _refreshMusicAspectDropdown(String newValue){
    setState(() => _musicAspect = newValue);
  }

  //aggregate function to output results based off of answers
  // does not quite work but i cannot figure out why
  void _toResultPage() {
    int _questionnaireResults = 0;

    if (_classical == true) {
      _questionnaireResults += 100;
    }
    if (_country == true) {
      _questionnaireResults += 200;
    }
    if (_classicRock == true) {
      _questionnaireResults += 300;
    }
    if (_christian == true) {
      _questionnaireResults += 400;
    }
    if (_pop == true) {
      _questionnaireResults += 500;
    }
    if (_heavyMetal == true) {
      _questionnaireResults += 600;
    }
    if (_rap == true) {
      _questionnaireResults += 700;
    }
    if (_metal == true) {
      _questionnaireResults += 800;
    }
    if (_alternative == true) {
      _questionnaireResults += 900;
    }
    if (_jazz == true) {
      _questionnaireResults += 1000;
    }
    if (_blues == true) {
      _questionnaireResults += 1100;
    }
    if (_itunes == true) {
      _questionnaireResults += 10;
    }
    if (_apple == true) {
      _questionnaireResults += 20;
    }
    if (_spotify == true) {
      _questionnaireResults += 30;
    }
    if (_youtube == true) {
      _questionnaireResults += 40;
    }
    if (_radio == true) {
      _questionnaireResults += 50;
    }
    if (_temp == true) {
      _questionnaireResults += 1;
    }
    if (_voice == true) {
      _questionnaireResults += 2;
    }
    if (_message == true) {
      _questionnaireResults += 3;
    }
    if (_instrument == true) {
      _questionnaireResults += 4;
    }

    //should take user page based off of answers... automatically takes user
    //to the third page
    if (_questionnaireResults > 501) {
      Navigator.push(
          context,
          MaterialPageRoute(
              builder: (context) => MySecondPage()));
    } else if (_questionnaireResults < 501) {
      Navigator.push(
          context,
          MaterialPageRoute(
              builder: (context) => MyThirdPage()));
    }else {
      Navigator.push(
          context,
          MaterialPageRoute(
              builder: (context) => MyFourthPage()));
    }
  }




  @override
  Widget build(BuildContext context) {
    return MaterialApp(
        home: Material(
          child: SingleChildScrollView(
            child: Column(
              children: <Widget>[
                Padding (
                    padding: EdgeInsets.all(25.0)
                ),
                // QUESTION ONE
                Text("1. What is your gender?", style: TextStyle
                  (color: Colors.black.withOpacity(1.0),
                    fontWeight: FontWeight.bold),),
                Row(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                      Radio(
                          value: 4, groupValue: _genderValue, onChanged: _refreshGenderValue),
                      Text("Male"),
                      Radio(
                          value: 5, groupValue: _genderValue, onChanged: _refreshGenderValue),
                      Text("Female"),

                      Radio(
                          value: 6, groupValue: _genderValue, onChanged: _refreshGenderValue),
                      Text("Prefer to not say")
                    ]),


                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),
                new Divider(height: 5.0, color: Colors.blueGrey),
                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),

                // QUESTION TWO
                Text("2. What is your age?", style: TextStyle
                  (color: Colors.black.withOpacity(1.0),
                    fontWeight: FontWeight.bold),),
                Row(),
                Row(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [
                      Radio(
                          value: 0, groupValue: _ageValue, onChanged: _refreshAgeValue),
                      Text('8-14'),
                      Radio(
                          value: 1, groupValue: _ageValue, onChanged: _refreshAgeValue),
                      Text('15-18'),
                      Radio(value: 2, groupValue: _ageValue, onChanged: _refreshAgeValue),
                      Text('19-25'),
                      Radio(value: 3, groupValue: _ageValue, onChanged: _refreshAgeValue),
                      Text('25-35'),

                    ]),
                Row(
                    mainAxisAlignment: MainAxisAlignment.center,
                    children: [

                      Radio(value: 4, groupValue: _ageValue, onChanged: _refreshAgeValue,),
                      Text('35 and older')
                    ]),


                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),
                new Divider(height: 5.0, color: Colors.blueGrey),
                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),

                // QUESTION THREE
                Text("3. What genre of music do you listen to the most?", style: TextStyle
                  (color: Colors.black.withOpacity(1.0),
                    fontWeight: FontWeight.bold),),
                Row(),
                DropdownButton<String>(
                  items: _listOfGenres, //_dropdownMenuItems,
                  onChanged: _refreshGenreKindDropdown,
                  value: _genreValue, // onChangeDropdownItem,
                  hint: Text("Select One"),
                ),
                Text(_genreValue != null
                    ? _genreValue
                    : "No Selection"),


                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),
                new Divider(height: 5.0, color: Colors.blueGrey),
                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),

                //QUESTION FIVE
                Text("4. What platform do you listen to music on?",  style: TextStyle
                  (color: Colors.black.withOpacity(1.0),
                    fontWeight: FontWeight.bold),),
                Row(),
                DropdownButton<String>(
                  items: _listOfMedium, //_dropdownMenuItems,
                  onChanged: _refreshMediumValueDropdown,
                  value: _mediumValue, // onChangeDropdownItem,
                  hint: Text("Select One"),
                ),
                Text(_mediumValue != null
                    ? _mediumValue
                    : "No Selection"),


                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),
                new Divider(height: 5.0, color: Colors.blueGrey),
                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),

                //QUESTION SIX
                Text("5. List the last three songs you chose to listen to most recently.", style: TextStyle
                  (color: Colors.black.withOpacity(1.0),
                    fontWeight: FontWeight.bold),),
                Row(),
                TextField(
                  controller: oneController,
                  obscureText: false,
                  textAlign: TextAlign.left,
                  decoration: InputDecoration(
                    border: InputBorder.none,
                    hintText: '1.',
                    hintStyle: TextStyle(color: Colors.grey),
                  ),
                ),
                TextField(
                  controller: twoController,
                  obscureText: false,
                  textAlign: TextAlign.left,
                  decoration: InputDecoration(
                    border: InputBorder.none,
                    hintText: '2.',
                    hintStyle: TextStyle(color: Colors.grey),
                  ),
                ),
                TextField(
                  controller: threeController,
                  obscureText: false,
                  textAlign: TextAlign.left,
                  decoration: InputDecoration(
                    border: InputBorder.none,
                    hintText: '3.',
                    hintStyle: TextStyle(color: Colors.grey),
                  ),
                ),


                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),
                new Divider(height: 5.0, color: Colors.blueGrey),
                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),

                //QUESTION SEVEN
                Text("6. What musical aspects do you enjoy most about the three songs you listed?", style: TextStyle
                  (color: Colors.black.withOpacity(1.0),
                    fontWeight: FontWeight.bold),),
                Row(),
                DropdownButton<String>(
                  items: _listOfMusic, //_dropdownMenuItems,
                  onChanged: _refreshMusicAspectDropdown,
                  value: _musicAspect, // onChangeDropdownItem,
                  hint: Text("Select One"),
                ),
                Text(_musicAspect != null
                    ? _musicAspect
                    : "No Selection"),

                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),
                new Divider(height: 5.0, color: Colors.blueGrey),
                new Padding(
                  padding: new EdgeInsets.all(8.0),
                ),

                RaisedButton(child: Text("Submit Questionnaire"), onPressed: _toResultPage


                )],
            ),
          ),
        ));
  }
}

class MySecondPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: new Color(0x673AB7),
          title: Text('Results'),
        ),
        body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text("What a cool music preference!"),
                RaisedButton(child: Text("Return to main screen"),  onPressed: (){
                  Navigator.of(context) .push(MaterialPageRoute<Null>(builder: (BuildContext context ) {
                    return new MyHomePage();
                  }));
                }
                )],
            )

        ));
  }

  MySecondPage();

}
class MyThirdPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: new Color(0x673AB7),
          title: Text('Results'),
        ),
        body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text("You have an interesting music preference!"),
                RaisedButton(child: Text("Return to main screen"),  onPressed: () {
                  Navigator.of(context).push(
                      MaterialPageRoute<Null>(builder: (BuildContext context) {
                        return new MyHomePage();
                      }));

                }
                )],
            )

        ));
  }

  MyThirdPage();

}

class MyFourthPage extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          backgroundColor: new Color(0x673AB7),
          title: Text('Results'),
        ),
        body: Center(
            child: Column(
              mainAxisAlignment: MainAxisAlignment.center,
              children: <Widget>[
                Text("error"),
                RaisedButton(child: Text("Return to main screen"),  onPressed: () {
                  Navigator.of(context).push(
                      MaterialPageRoute<Null>(builder: (BuildContext context) {
                        return new MyHomePage();
                      }));
                }
                )],
            )

        ));
  }

  MyFourthPage();

}



