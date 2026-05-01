https://github.com/resatarruk-maker/Tyt-1ay.gitimport 'package:flutter/material.dart';
import 'package:webview_flutter/webview_flutter.dart';

void main() {
  runApp(MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      home: WebApp(),
    );
  }
}

class WebApp extends StatefulWidget {
  @override
  _WebAppState createState() => _WebAppState();
}

class _WebAppState extends State<WebApp> {
  late final WebViewController controller;

  @override
  void initState() {
    super.initState();

    controller = WebViewController()
      ..setJavaScriptMode(JavaScriptMode.unrestricted)
      ..loadHtmlString('''
<!DOCTYPE html>
<html>
<head>
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<style>
body { font-family: Arial; text-align: center; }
button { margin: 10px; padding: 10px; }
</style>
</head>
<body>

<h2>TYT Test</h2>
<p id="q"></p>
<div id="answers"></div>

<script>
const questions = [
  {q:"2+2=?", a:["3","4","5"], correct:1},
  {q:"Capital of Turkey?", a:["Istanbul","Ankara","Izmir"], correct:1}
];

let i=0, score=0;

function loadQ(){
  let q = questions[i];
  document.getElementById("q").innerText = q.q;
  let html="";
  q.a.forEach((ans,index)=>{
    html += "<button onclick='check("+index+")'>"+ans+"</button>";
  });
  document.getElementById("answers").innerHTML = html;
}

function check(index){
  if(index===questions[i].correct) score++;
  i++;
  if(i<questions.length) loadQ();
  else document.body.innerHTML="<h2>Score: "+score+"</h2>";
}

loadQ();
</script>

</body>
</html>
      ''');
  }

  @override
  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(title: Text("TYT App")),
      body: WebViewWidget(controller: controller),
    );
  }
}# Tyt-1ay
Tyt  1 ayda bitremek
