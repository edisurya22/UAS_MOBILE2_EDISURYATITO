# UAS_MOBILE2_EDISURYATITO
import 'package:flutter/material.dart';

void main() => runApp(App04());

class App04 extends StatelessWidget {
  Widget build(BuildContext context) {
    return MaterialApp(
      routes: {
        "Data": (context) => EdiSuryaTitoDataTable(),
        "Lupa": (context) => LupaPass(),
        "aritmatika": (context) => Aritmatika(),
      },
      title: 'FORM LOGIN',
      home: Scaffold(
        appBar: AppBar(
          title: Text('UAS- Edi Surya Tito (6SIA4)'),
        ),
        body: LoginPage(),
      ),
    );
  }
}

class LoginPage extends StatefulWidget {
  _LoginPageState createState() => new _LoginPageState();
}

class _LoginPageState extends State<LoginPage> {
  final myNirm = TextEditingController();

  String nirm;

  onLogin() {
    nirm = myNirm.text;
    if (nirm == '2018020300') {
      Navigator.pushNamed(context, "Data");
    } else {
      Navigator.pushNamed(context, "Lupa");
    }
  }

  Widget build(BuildContext context) {
    final id = TextFormField(
      keyboardType: TextInputType.emailAddress,
      autofocus: false,
      controller: myNirm,
      decoration: InputDecoration(
        icon: Icon(Icons.person, color: Colors.blue),
        hintText: 'NIRM',
        contentPadding: EdgeInsets.fromLTRB(20.0, 10.0, 20.0, 10.0),
        border: OutlineInputBorder(borderRadius: BorderRadius.circular(32.0)),
      ),
    );

    final loginButton = Padding(
      padding: EdgeInsets.symmetric(vertical: 16.0),
      child: Material(
        borderRadius: BorderRadius.circular(30.0),
        shadowColor: Colors.lightBlueAccent.shade100,
        elevation: 5.0,
        child: MaterialButton(
          minWidth: 200.0,
          height: 42.0,
          onPressed: onLogin,
          // () {Navigator.pushNamed(context, "myApp");},
          color: Colors.lightBlueAccent,
          child: Text('Masuk', style: TextStyle(color: Colors.white)),
        ),
      ),
    );

    return Scaffold(
      backgroundColor: Colors.white,
      body: Center(
        child: ListView(
          shrinkWrap: true,
          padding: EdgeInsets.only(left: 24.0, right: 24.0),
          children: <Widget>[
            SizedBox(height: 48.0),
            id,
            SizedBox(height: 8.0),
            loginButton,
          ],
        ),
      ),
    );
  }
}

class LupaPass extends StatelessWidget {
  Widget build(BuildContext context) {
    return Scaffold(
        appBar: AppBar(
          title: Text('Lupa NIRM'),
        ),
        //body
        body: Text("Nirm Yang Anda Masukkan Salah"));
  }
}

class EdisuryatitoDataTable extends StatefulWidget {
  _EdisuryatitoDataTableState createState() =>
      _EdisuryatitoDataTableState();
}

class _EdisuryatitoDataTableState
    extends State<EdiSuryaDataTable> {
  List<DataMahasiswa> barang;

  void initState() {
    super.initState();
    barang = DataMahasiswa.getDataBarang();
  }

  Widget build(BuildContext context) {
    return Scaffold(
      appBar: AppBar(
        title: Text('Edi Surya Tito - 6SIA4'),
      ),
      body: ListView(children: <Widget>[
        Center(
            child: Text('Data Mahasiswa',
                style: TextStyle(fontSize: 20, fontWeight: FontWeight.bold))),
        DataTable(
          columns: [
            DataColumn(label: Text('')),
            DataColumn(label: Text('')),
          ],
          rows: barang
              .map(
                (barang) => DataRow(cells: [
                  DataCell(Text(barang.id)),
                  DataCell(Text(barang.namabarang)),
                ]),
              )
              .toList(),
        ),
        Padding(
          padding: EdgeInsets.symmetric(vertical: 16.0),
          child: Material(
            borderRadius: BorderRadius.circular(30.0),
            shadowColor: Colors.lightBlueAccent.shade100,
            elevation: 5.0,
            child: MaterialButton(
              minWidth: 200.0,
              height: 42.0,
              onPressed: () {
                Navigator.pushNamed(context
