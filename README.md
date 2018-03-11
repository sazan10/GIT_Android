### Permanent Storage(Local) using Sharedpreferences

----

----
```
SharedPreferences sharedp=this.getSharedPrefereces("package_name",Context.MODE_PRIVATE) 
```
Mode private allows only this app to use the data

```
sharedp.edit().putString("username","rob").apply();
```
to save string rob under variable name username

``` 
String username=sharedp.getString("username","");
```
Retrieves the value for variable username


### Display output in Logcat
----

----
```
Log.i("tag","output_to_display");
```

### Button click
----

----
For the button in xml mode assign function name and implement it in main activity
```
public void onButtonClick(View view)
{
}
```

### GridLayout
----

----
While working with gridview drag gridview and then other elements into grid. Then use rows and columns to label them. On clicking the items in grid view they all may point to same function however using the ids we can perform task as required. 
```
public void buttonTapped(View view)
	{
	int id=view.getId();
	String ourId="";
	ourId=view.getResources().getResourceEntryName(id); //returns id 
	--to recieve location
	int resourceId=getResources().getIdentifier(ourId,"row","package_name");
	}
	
### Animations
----

----
ImageView a= fvbid
```
a.animate().alpha(value).rotationY(value).translationYBy(value).setDuration(value);

### ListView
----

----
ListView requires an arrayList for data
```
ListView myListView= fvbid... 
ArrayList<String> data=new ArrayList<String>();
data.add("ddd");
```
Then arrayAdapter is required to map arrayList into ListView
```
ArrayAdapter <String> arrayAdapter = new ArrayAdapter<String>(this,android.R.layout.simple_list_item_1,data);
myListView.setAdapter(arrayAdapter);
myListView.setOnItemClickListener(new AdapterView..)
```

### Downloading data from internet(HTML code)
----
 
----
```public class DownloadTask extends AsyncTask<String{input for DownloadTask, eg url}, Void{progress bar for downloads},String {data return type}>
```
Implement method doInBackground
```protected String doInBackground(String... urls)
	{
	url=new URL(urls[0]);
	urlConnection=(HttpURLConnection) url.openConnection();
	InputStream in =urlConnection.getInputStream();
	InputStreamReader reader = new InputStreamReader(in);
	int data = reader.read();
	while(data!=-1){
	char current =(char) data;
	result+=current;
	data=reader.read();
	}
	return result;
```
Then create object of DownloadTask and execute with url as argument
```
object.execute("url").get();
```

### Downloading image from internet
Similar to downloading web content however we downloaded all the characters one by one and combined them. In this case, we download the image in one go and convert the data into bitmap image for for return type it will be Bitmap.
```
	URL url = new URL(urls[0]);
	HttpURLConnection connection = (HttpURLConnection) url.openConnection();
	connection.connect();
	InputStream inputStream=connection.getInputStream(;
	Bitmap myBitmap=BItmapFactory.decodeStream(inputStream);
	return myBitmap;
```

### Processing JSON Data
```
JSONObject jsonObject = new JSONObject(result);
String string_name1=jsonObject.getString("label");
```
For multi level JSON
```
JSONArray arr= new JSONArray(string_name1
for loop
{
JSONObject j= arr.getJSONObject(i);
}
```
----

----

### Alert Dialogs

```
new AlertDialog.Builder(this).setIcon(android.R.drawable.ic_kdj).setTitle("Are you sure").setMessage("Do you really want to do this").setPositiveButton("yes",new DialogInterface.OnClickListener(){
pv onClick()}).setNegativeButton("no",null).show();
```

### Start Activity Using Intent
----

----
```
Intent i = new Intent(getApplicationContext(),secondActivity.class);
startActivity(i);

```

### SQLite
Create database
```
SQLiteDatabase myDatabase = this.openOrCreateDatabase("Database_name",MODE_PRIVATE,null);
```
Create Table and insert into table
```
myDatabase.execSQL("CREATE TABLE IF NOT EXISTS users (name VARCHAR, age INT(3))");
myDatabase.execSQL("INSERT INTO users (name,age) VALUES ("Rob",34)");
```
Execute select query. Here we also need to deal with indexes

```
Cursor c = myDatabase.rawQuery("SELECT * FROM users", null);
int nameindex =c.getColumnIndex("name");
int ageIndex=c.getColumnIndex("age");
c.moveToFirst();
while (c!=null){
c.getString(nameIndex));
Integer.toString(c.getInt(ageIndex)));
c.moveToNext();
}
``` 
----

----

### WebViews
Webviews are ways to show websites via app
```
WebView web= fvid();
web.getSettings().setJavaScriptEnabled(true);
 web.setWebViewClient(new WebViewClient());
web.loadUrl("www.google.com");
```
Without setwebviewclient chrome will be used.

----

----
### Bluetooth

It requires a bluetooth adapter.
```
BluetoothAdapter Ba;
```
To check if bluetooth is on
```
Ba.isEnabled()
```
To enable bluetooth
```
Intent i = new Intent (BluetoothAdapter.ACTION_REQUEST_ENABLE);
startActivity(i);
```
To Disable bluetooth
```
Ba.disable();
```
To view the paired devices 
Firstly we need to define a set and convert it into an array list for the array adapter to diplay it in listview

```
Set <BluetoothDevice> pairedDevices=Ba.getBondedDevices();
ListView pairedDevicesListView =(ListView) findViewById(R.id.pairedDevicesListView);
ArrayList pairedDevicesArrayList = new ArrayList();
for(BluetoothDevice bluetoothDevice:pairedDevices)
{
pairedDevicesArrayList.add(bluetoothDevice.getName());
}
ArrayAdapter arrayAdapter=new ArrayAdapter(this, android.R.layout.simple_list_item_1,pairedDevicesArrayList);
pairedDeviesListView.setAdapter(arrayAdapter);
```

### Ads
It needs google repository SDK and need to add the following in build.gradle file:
```
compile 'com.google.android.gms:play-services-ads:7.8.0'

```
Then we need to edit the manifest file adding necessary permissions for internet and access network state. Also add metadata to parse google play services version and add activity to add the ad into and set various settings as required.

```
 <meta-data android:name="com.google.android.gms.version" android:value="@integer/google_play_services_version"/>
  <activity android:name="com.google.android.gms.ads.AdActivity"  android:theme="@android:style/Theme.Translucent" />

```

In activityMain.xml add namespace for the add and code for adVIew and in MainActivity create adView and Request.     
    banner_ad_unit_id: ca-app-pub-3940256099942544/1033173712 

```
xml file 
xmlns:ads="http://schemas.android.com/apk/res-auto"

<com.google.android.gms.ads.AdView
        android:id="@+id/adView"
        android:layout_width="fill_parent"
        android:layout_height="wrap_content"

        android:layout_alignParentBottom="true"
        android:layout_centerHorizontal="true"
        ads:adSize="BANNER"
        ads:adUnitId="@string/banner_ad_unit_id">
    </com.google.android.gms.ads.AdView>

Java file
 AdView adView=(AdView) findViewById(R.id.adView);
        AdRequest adRequest=new AdRequest.Builder().build();
        adView.loadAd(adRequest);
        
```

### Notifications
setContentIntent is used for what happens if the notification is tapped for which we need pending intent. Which notiifcation is tapped on is given by the second parameter(integer). addAction for button 
```

Intent = intent = new Intent(getApplicatonContext(),MainActivity.class);
PendingIntent pendingIntent= PendingIntent.getActivity(getApplicationContext(),1, intent,0);
Notification notification =new Notification.Builder(getApplicationContext()).setContentTitle("").setContentText("").setSmallIcon(R.draw.) .setContentIntent(pendingIntent).addAction(android.R.id.drawable,"name",pendingIntent).setSmallIcon(android.R.drawable).build();
NotificationManager not=(NotificationManager) getSystemService(NOTIFICATION_SERVICE);
not.notify(integer,notification);
```

----

----

### Parse

#### Setup


First install parse server as instructed in:
```
https://tecadmin.net/install-parse-server-on-ubuntu/
```
###
Create android project for parse or download as required. Then Create mLab account, add user and create new database. 
Create Heroku app and set environment variable. Variable as required from the parse server instruction in index.js and uri as given by mLab on creating database.
```
DATABASE_URI="mongodb://<dbuser>:<dbpassword>@ds263138.mlab.com:63138/parse"

```  
Set heroku git url as remote and push the parse-server-example from above setup installation to heroku. Now it should work on android after modifying the variables as required and for server use "/" at the end.
 
 
 ----
 
 ----
 
#### Parse Basics
```
Parse.enableLocalDatastore(this);

    // Add your initialization code here
    Parse.initialize(new Parse.Configuration.Builder(getApplicationContext())
            .applicationId("KSJ4KLJ5KJK435J3KSS9F9D8S9F8SD98F9SDF")
            .clientKey("KSJFKKJ3K4JK3J4K3JUWE89ISDJHFSJDFS")
            .server("https://parsetestandroid.herokuapp.com/parse/")

            .build());

      ParseObject gameScore = new ParseObject("GameScore");
      gameScore.put("scorerr", 234322);
      gameScore.put("playerName", "Sean Plott");
      gameScore.put("cheatMode", false);
      gameScore.saveInBackground() 
```
### Menu

In menu xml file context is required and item as shown:
```
tools:context="com.parse.starter.UserList"
 <item android:id="@+id/share" android:title="share" app:showAsAction="always"/>

```
The item is access in onOptionsItemSelected:
```
 @Override
    public boolean onCreateOptionsMenu(Menu menu)
    {
        getMenuInflater().inflate(R.menu.user_list_menu,menu);
        return true;
    }
    @Override
    public boolean onOptionsItemSelected(MenuItem item)
    {
        int id =item.getItemId();
        if(id==R.id.share)
        {
            Intent i = new Intent(Intent.ACTION_PICK, MediaStore.Images.Media.EXTERNAL_CONTENT_URI);
            startActivityForResult(i,1);

            return true;
        }
    return super.onOptionsItemSelected(item);
    }
```

### Importing image from disk and sending it to parse
The startActivityForResult from above expects onActivityResult(). For seding image to parse we need to convert it firstly into a byte array and then into a file 

```
@Override
    protected void onActivityResult(int requestCode, int resultCode, Intent data) {
        super.onActivityResult(requestCode, resultCode, data);
    if(requestCode==1 && resultCode==RESULT_OK && data!=null)
    {
        Uri selectedImage=data.getData();
        try {
            Bitmap bitmap=MediaStore.Images.Media.getBitmap(this.getContentResolver(),selectedImage);//get bitmap from mediastore, here image which is selected
            Toast.makeText(getApplicationContext(),"Image Received",Toast.LENGTH_LONG).show();
            //ImageView imageView= findViewById(R.id.imag);
            //imageView.setImageBitmap(bitmap);
            ByteArrayOutputStream stream =new ByteArrayOutputStream();//stream convert image to byte array
            bitmap.compress(Bitmap.CompressFormat.PNG,100,stream);//compress bitmap image into png, with quality 100 using stream output stream
            byte [] byteArray =stream.toByteArray();//converting stream to bytearray
            ParseObject object =new ParseObject("images");//Create parse object "images"
            ParseFile file = new ParseFile("image.png",byteArray);//convert byteArray to file to store in Parse
            object.put("username",ParseUser.getCurrentUser().getUsername());//put username value in "username" field(column) for currently logged in username
            object.put("image",file);
            object.saveInBackground(new SaveCallback() {
                @Override
                public void done(ParseException e) {
                    if(e==null)
                    {
                        Toast.makeText(getBaseContext(),"your image has been posted",Toast.LENGTH_LONG).show();
                    }
                    else
                        Toast.makeText(getApplicationContext(),"Your image cannot be posted",Toast.LENGTH_LONG).show();
                }
            });
        } catch (IOException e) {
            e.printStackTrace();
            Toast.makeText(getApplicationContext(),"there was an error",Toast.LENGTH_LONG).show();
        }
    }
    }
```



