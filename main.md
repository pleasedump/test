Ex – 01: BMI Calculator
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/main"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<EditText
android:id="@+id/weightInput"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="Enter weight (kg)"
android:inputType="numberDecimal"
app:layout_constraintBottom_toTopOf="@+id/heightInput"
app:layout_constraintTop_toTopOf="parent"
app:layout_constraintVertical_bias="0.401"
tools:ignore="MissingConstraints"
tools:layout_editor_absoluteX="0dp" />
<EditText
android:id="@+id/heightInput"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_marginBottom="60dp"
android:hint="Enter height (m)"
android:inputType="numberDecimal"
app:layout_constraintBottom_toTopOf="@+id/calculateButton"
tools:ignore="MissingConstraints"
tools:layout_editor_absoluteX="0dp" />
<Button
android:id="@+id/calculateButton"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_marginBottom="176dp"
android:text="Calculate BMI"
app:layout_constraintBottom_toTopOf="@+id/resultTextView"
tools:ignore="MissingConstraints"
tools:layout_editor_absoluteX="0dp" />
<TextView
android:id="@+id/resultTextView"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_marginBottom="212dp"
android:paddingTop="16dp"
android:text=""
android:textSize="18sp"
app:layout_constraintBottom_toBottomOf="parent"
tools:ignore="MissingConstraints"
tools:layout_editor_absoluteX="16dp" />
</androidx.constraintlayout.widget.ConstraintLayout>

MainActivity.kt
import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import android.widget.TextView
import androidx.activity.enableEdgeToEdge
import androidx.appcompat.app.AppCompatActivity
import androidx.core.view.ViewCompat
import androidx.core.view.WindowInsetsCompat
class MainActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
enableEdgeToEdge()
setContentView(R.layout.activity_main)
val weight:EditText = findViewById(R.id.w)
val height:EditText = findViewById(R.id.h)
val btn: Button = findViewById(R.id.btn)
val tv:TextView = findViewById(R.id.result)
btn.setOnClickListener{
val w = weight.text.toString().toFloat()
val h = height.text.toString().toFloat()
val bmi = w / (h*h)
val cat = when {
bmi < 18.0 -> "Underweight"
bmi in 18.0..24.0 -> "Normal"
bmi in 25.0..30.0 -> "Overweight"
else -> "Obese"
}
tv.text = "BMI = $bmi \nCategory = $cat"
}
}

}

Example output:

User Input:
•
•

Weight: 70 kg
Height: 1.75 m

BMI: 22.86 Status: Normal

Must Know
Using implicit intent
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/main"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<EditText
android:id="@+id/nameInput"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="Enter your name"
android:inputType="textPersonName"
app:layout_constraintBottom_toTopOf="@+id/goNextActBtn"
app:layout_constraintTop_toTopOf="parent"
tools:layout_editor_absoluteX="-80dp" />
<Button
android:id="@+id/goNextActBtn"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_marginBottom="316dp"
android:text="Calculate BMI"
app:layout_constraintBottom_toBottomOf="parent"
tools:ignore="MissingConstraints"
tools:layout_editor_absoluteX="-16dp" />
</androidx.constraintlayout.widget.ConstraintLayout>

MainActivity.kt
import android.content.Intent
import android.os.Bundle
import android.widget.Button
import android.widget.EditText
import androidx.appcompat.app.AppCompatActivity
class MainActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
val nameInput: EditText = findViewById(R.id.nameInput)
val goNextActBtn: Button = findViewById(R.id.goNextActBtn)
goNextActBtn.setOnClickListener {
val name = nameInput.text.toString()

}
}

}

// Pass the name to ResultActivity
val intent = Intent(this, ResultActivity::class.java)
intent.putExtra("NAME", name)
startActivity(intent)

result_activity.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/main"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".ResultActivity">
<TextView
android:id="@+id/resultTextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>

ResultActivity.kt
import android.os.Bundle
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
class ResultActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_result)
val resultTextView: TextView = findViewById(R.id.resultTextView)

}

}

val name = intent.getStringExtra("NAME")
resultTextView.text = "$name"

Must Know
Using explicit intent (can be used for EX 08 sending mail or sms)
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/main"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<Button
android:id="@+id/openPhoneAppButton"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Open Phone App"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
</androidx.constraintlayout.widget.ConstraintLayout>
MainActivity.kt (for opening phone)
import android.content.Intent
import android.net.Uri
import android.os.Bundle
import android.widget.Button
import androidx.appcompat.app.AppCompatActivity
class MainActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
val MyButton: Button = findViewById(R.id.openPhoneAppButton)
MyButton.setOnClickListener{
val intent = Intent(Intent.ACTION_DIAL)
intent.data = Uri.parse("tel: 9080819643")
startActivity(intent)
}
}

}

(for opening Mail app)
btn.setOnClickListener{
val intent = Intent(Intent.ACTION_SENDTO)
intent.data = Uri.parse("mailto: sam@karunya.edu.in")
startActivity(intent)
}
(for opening SMS app)
btn.setOnClickListener{
val intent = Intent(Intent.ACTION_VIEW)
intent.data = Uri.parse("sms: 9080819643")
intent.putExtra("sms_body", "It is critical")
startActivity(intent)
}

Ex – 02: Widgets
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:id="@+id/main"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<CheckBox
android:id="@+id/checkBox"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Check me"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toTopOf="parent" />
<RadioGroup
android:id="@+id/radioGroup"
android:layout_width="match_parent"
android:layout_height="wrap_content"
app:layout_constraintBottom_toTopOf="@+id/spinner"
app:layout_constraintTop_toBottomOf="@+id/checkBox"
app:layout_constraintVertical_bias="0.0"
tools:layout_editor_absoluteX="16dp">
<RadioButton
android:id="@+id/radioButton1"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Option A" />
<RadioButton
android:id="@+id/radioButton2"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Option B" />
</RadioGroup>
<Spinner
android:id="@+id/spinner"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_marginTop="168dp"
app:layout_constraintTop_toBottomOf="@+id/checkBox"
tools:layout_editor_absoluteX="0dp" />
<Switch
android:id="@+id/switchToggle"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Toggle switch"
app:layout_constraintBottom_toTopOf="@+id/displayButton"
app:layout_constraintEnd_toEndOf="parent"
app:layout_constraintStart_toStartOf="parent"
app:layout_constraintTop_toBottomOf="@+id/spinner" />
<Button
android:id="@+id/displayButton"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:layout_marginTop="200dp"

android:text="Display Selections"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintTop_toBottomOf="@+id/spinner"
tools:layout_editor_absoluteX="0dp" />
<TextView
android:id="@+id/resultTextView"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:paddingTop="16dp"
android:textSize="16sp"
app:layout_constraintBottom_toBottomOf="parent"
app:layout_constraintTop_toBottomOf="@+id/displayButton"
tools:layout_editor_absoluteX="0dp" />
</androidx.constraintlayout.widget.ConstraintLayout>

MainActivity.kt
import android.os.Bundle
import android.widget.*
import androidx.appcompat.app.AppCompatActivity
class MainActivity : AppCompatActivity() {
@SuppressLint("MissingInflatedId")
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
val checkBox: CheckBox = findViewById(R.id.checkBox)
val radioGroup: RadioGroup = findViewById(R.id.radiogroup)
val spinner: Spinner = findViewById(R.id.spinner)
val switchToggle: Switch = findViewById(R.id.switch1)
val btn: Button = findViewById(R.id.btn)
val resultTextView: TextView = findViewById(R.id.tv)
val items = arrayOf("item1", "item2", "item3")
val adapter = ArrayAdapter(this, android.R.layout.simple_spinner_item, items)
spinner.adapter = adapter
btn.setOnClickListener{
val c = if(checkBox.isChecked) "Checked" else "Not Checked"
val RR = radioGroup.checkedRadioButtonId
val R = findViewById<RadioButton>(RR).text.toString()
val sp = spinner.selectedItem.toString()
val sw = if(switchToggle.isChecked) "On" else "Off"
}

}

}

resultTextView.text = " C => $c \nR => $R \nsp => $sp \nsw => $sw"

Ex – 03: List View
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.constraintlayout.widget.ConstraintLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<ListView
android:id="@+id/listView"
android:layout_width="match_parent"
android:layout_height="match_parent" />
</androidx.constraintlayout.widget.ConstraintLayout>

list_item.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:orientation="horizontal"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:padding="8dp">
<ImageView
android:id="@+id/imageView"
android:layout_width="50dp"
android:layout_height="50dp"
android:layout_marginEnd="8dp"
android:src="@drawable/ic_launcher_foreground" />
<LinearLayout
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:orientation="vertical">
<TextView
android:id="@+id/titleTextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Title"
android:textStyle="bold"
android:textSize="16sp" />
<TextView
android:id="@+id/descriptionTextView"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Description"
android:textSize="14sp" />
</LinearLayout>
</LinearLayout>
Item.kt
data class Item(val imageResId: Int, val title: String, val description: String)

MainActivity.kt
import android.os.Bundle
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.ArrayAdapter
import android.widget.ImageView
import android.widget.ListView
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
class MainActivity : AppCompatActivity() {
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
val listView: ListView = findViewById(R.id.listView)
val items = listOf(
Item(R.drawable.ic_launcher_background, "Title 1", "Description 1"),
Item(R.drawable.ic_launcher_background, "Title 2", "Description 2"),
Item(R.drawable.ic_launcher_background, "Title 3", "Description 3")
)
val adapter = object : ArrayAdapter<Item>(this, R.layout.list_item, items) {
override fun getView(position: Int, convertView: View?, parent: ViewGroup):
View {
val view = convertView ?: LayoutInflater.from(context)
.inflate(R.layout.list_item, parent, false)
val item = getItem(position)!!
view.findViewById<ImageView>(R.id.imageView)
.setImageResource(item.imageResId)
view.findViewById<TextView>(R.id.titleTextView).text = item.title
view.findViewById<TextView>(R.id.descriptionTextView)
.text = item.description
}

return view

}

}

}

listView.adapter = adapter

Ex – 04: SQL lite
Here's an Android app that uses SQLite to store items entered by the user, and displays
the items in a ListView. When a user clicks on an item, it gets deleted, and when the
item is long pressed, it also gets deleted.
ItemAdapter.kt
import android.content.Context
import android.view.LayoutInflater
import android.view.View
import android.view.ViewGroup
import android.widget.TextView
import android.widget.Toast
import android.widget.AdapterView
import android.widget.BaseAdapter
class ItemAdapter(private val context: Context, private val items: MutableList<String>,
private val dbHelper: DatabaseHelper) : BaseAdapter() {
override fun getCount(): Int = items.size
override fun getItem(position: Int): Any = items[position]
override fun getItemId(position: Int): Long = position.toLong()
override fun getView(position: Int, convertView: View?, parent: ViewGroup?): View {
val view = convertView ?: LayoutInflater.from(context)
.inflate(android.R.layout.simple_list_item_1,
parent, false)
val itemTextView: TextView = view.findViewById(android.R.id.text1)
val item = items[position]
itemTextView.text = item
view.setOnLongClickListener {
// Handle long press: delete item
val itemId = position + 1
dbHelper.deleteItem(itemId)
items.removeAt(position)
notifyDataSetChanged()
Toast.makeText(context, "Item deleted", Toast.LENGTH_SHORT).show()
true
}
return view
}

}

DatabaseHelper.kt
import android.content.ContentValues
import android.content.Context
import android.database.Cursor
import android.database.sqlite.SQLiteDatabase
import android.database.sqlite.SQLiteOpenHelper

class DatabaseHelper(context: Context) : SQLiteOpenHelper(context, DATABASE_NAME, null,
DATABASE_VERSION) {
companion object {
const val DATABASE_NAME = "items.db"
const val DATABASE_VERSION = 1
const val TABLE_NAME = "items"
const val COLUMN_ID = "id"
const val COLUMN_NAME = "name"
}
override fun onCreate(db: SQLiteDatabase?) {
val CREATE_TABLE = """
CREATE TABLE IF NOT EXISTS $TABLE_NAME (
$COLUMN_ID INTEGER PRIMARY KEY AUTOINCREMENT,
$COLUMN_NAME TEXT
);
"""
db?.execSQL(CREATE_TABLE)
}
override fun onUpgrade(db: SQLiteDatabase?, oldVersion: Int, newVersion: Int) {
val DROP_TABLE = "DROP TABLE IF EXISTS $TABLE_NAME"
db?.execSQL(DROP_TABLE)
onCreate(db)
}
// Insert a new item into the database
fun addItem(itemName: String): Long {
val db = writableDatabase
val contentValues = ContentValues().apply {
put(COLUMN_NAME, itemName)
}
return db.insert(TABLE_NAME, null, contentValues)
}
// Get all items from the database
fun getAllItems(): Cursor {
val db = readableDatabase
return db.query(
TABLE_NAME,
arrayOf(COLUMN_ID, COLUMN_NAME), // Column names to fetch
null,
null,
null,
null,
null
)
}
// Delete an item by its ID
fun deleteItem(id: Int): Int {
val db = writableDatabase
return db.delete(TABLE_NAME, "$COLUMN_ID = ?", arrayOf(id.toString()))
}
fun updateItem(id: Int, newItem: String): Int {
val db = writableDatabase
val contentValues = ContentValues().apply {
put(COLUMN_NAME, newItem)
}
return db.update(TABLE_NAME, contentValues,
"$COLUMN_ID = ?", arrayOf(id.toString()))
}

}
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
android:padding="16dp">
<!-- EditText for item input -->
<EditText
android:id="@+id/itemEditText"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:hint="Enter item name"
android:inputType="text" />
<!-- Button to save updated item name -->
<Button
android:id="@+id/saveButton"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Save Changes" />
<!-- ListView to display items -->
<ListView
android:id="@+id/listView"
android:layout_width="match_parent"
android:layout_height="wrap_content" />
</LinearLayout>
MainActivity.kt
import android.database.Cursor
import android.os.Bundle
import android.view.View
import android.widget.AdapterView
import android.widget.ArrayAdapter
import android.widget.Button
import android.widget.EditText
import android.widget.ListView
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
class MainActivity : AppCompatActivity() {
private lateinit var dbHelper: DatabaseHelper
private lateinit var itemEditText: EditText
private lateinit var saveButton: Button
private lateinit var listView: ListView
private lateinit var itemsList: ArrayList<String>
private lateinit var adapter: ArrayAdapter<String>
private var currentItemId: Int = -1 // Store the ID of the item being edited
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
dbHelper = DatabaseHelper(this)
itemEditText = findViewById(R.id.itemEditText)
saveButton = findViewById(R.id.saveButton) // Button to save the changes
listView = findViewById(R.id.listView)

itemsList = ArrayList()

// Set up the ListView
adapter = ArrayAdapter(this, android.R.layout.simple_list_item_1, itemsList)
listView.adapter = adapter
// Load items from the database
loadItems()
// Button click listener to save changes to the item
saveButton.setOnClickListener {
val updatedText = itemEditText.text.toString().trim()
if (updatedText.isNotEmpty()) {
if (currentItemId == -1) {
// If no item is being edited, add a new item
// Insert new item into the database
val newItem = dbHelper.addItem(updatedText)
if (newItem != -1L) {
Toast.makeText(this, "Item added!", Toast.LENGTH_SHORT).show()
itemEditText.text.clear()
loadItems() // Refresh the list
}
} else { // If an item is being edited, update the item
val rowsUpdated = dbHelper.updateItem(currentItemId, updatedText)
if (rowsUpdated > 0) {
Toast.makeText(this, "Item updated!",
Toast.LENGTH_SHORT).show()
itemEditText.text.clear()
currentItemId = -1
loadItems() // Refresh the list
}
}
} else {
Toast.makeText(this, "Please enter a valid item name.",
Toast.LENGTH_SHORT).show()
}
}
// Set up ListView item click listener to allow editing the item
listView.setOnItemClickListener { _, _, position, _ ->
val cursor = dbHelper.getAllItems()
cursor.moveToPosition(position)
val id = cursor.getInt(cursor.getColumnIndex(DatabaseHelper.COLUMN_ID))
val currentItemName = cursor.getString(cursor.
getColumnIndex(DatabaseHelper.COLUMN_NAME))

}

// Set the current item name in the EditText for editing
itemEditText.setText(currentItemName)
currentItemId = id // Store the ID of the item being edited
cursor.close()

// Set up long click listener to delete item
listView.setOnItemLongClickListener { _, _, position, _ ->
val cursor = dbHelper.getAllItems()
cursor.moveToPosition(position)
val id = cursor.getInt(cursor.getColumnIndex(DatabaseHelper.COLUMN_ID))
val deletedRows = dbHelper.deleteItem(id)
if (deletedRows > 0) {
Toast.makeText(this, "Item deleted!", Toast.LENGTH_SHORT).show()
loadItems() // Refresh the list
}
cursor.close()
true

}

}

}

// Load items from the database and update the ListView
private fun loadItems() {
val cursor: Cursor = dbHelper.getAllItems()
itemsList.clear()
if (cursor.moveToFirst()) {
do {
val itemName = cursor.getString(cursor
.getColumnIndex(DatabaseHelper.COLUMN_NAME))
itemsList.add(itemName)
} while (cursor.moveToNext())
}
cursor.close()
adapter.notifyDataSetChanged()
}

To be added in AndroidManifest.xml
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"/>
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE"/>

Ex – 05: Content Providers
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
android:padding="16dp">
<!-- Button to fetch contacts -->
<Button
android:id="@+id/btnContacts"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Fetch Contacts" />
<!-- Button to fetch SMS messages -->
<Button
android:id="@+id/btnSms"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Fetch SMS" />
<!-- TextView to display the fetched data -->
<TextView
android:id="@+id/tvOutput"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:text="Data will appear here"
android:paddingTop="16dp"
android:scrollbars="vertical" />
</LinearLayout>

MainActivity.kt
import android.Manifest
import android.content.ContentResolver
import android.content.pm.PackageManager
import android.net.Uri
import android.os.Bundle
import android.provider.ContactsContract
import android.provider.Telephony
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
import androidx.core.app.ActivityCompat
import androidx.core.content.ContextCompat
class MainActivity : AppCompatActivity() {
private lateinit var btnContacts: Button
private lateinit var btnSms: Button
private lateinit var tvOutput: TextView
companion object {
const val REQUEST_CONTACTS_PERMISSION = 100
const val REQUEST_SMS_PERMISSION = 101
}
override fun onCreate(savedInstanceState: Bundle?) {

super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
btnContacts = findViewById(R.id.btnContacts)
btnSms = findViewById(R.id.btnSms)
tvOutput = findViewById(R.id.tvOutput)
btnContacts.setOnClickListener {
checkPermission(Manifest.permission.READ_CONTACTS,
REQUEST_CONTACTS_PERMISSION) {
fetchContacts()
}
}

}

btnSms.setOnClickListener {
checkPermission(Manifest.permission.READ_SMS, REQUEST_SMS_PERMISSION) {
fetchSmsMessages()
}
}

private fun checkPermission(permission: String, requestCode: Int, onGranted: () ->
Unit) {
if (ContextCompat.checkSelfPermission(this, permission) ==
PackageManager.PERMISSION_GRANTED) {
onGranted()
} else {
ActivityCompat.requestPermissions(this, arrayOf(permission), requestCode)
}
}
private fun fetchContacts() {
val contentResolver: ContentResolver = contentResolver
val uri: Uri = ContactsContract.CommonDataKinds.Phone.CONTENT_URI
val cursor = contentResolver.query(uri, null, null, null, null)
val stringBuilder = StringBuilder()
cursor?.let {
while (it.moveToNext()) {
val name = it.getString(it.getColumnIndex(ContactsContract
.CommonDataKinds.Phone.DISPLAY_NAME))
val phoneNumber = it.getString(it.getColumnIndex(ContactsContract
.CommonDataKinds.Phone.NUMBER))
stringBuilder.append("Name: $name\nPhone: $phoneNumber\n\n")
}
it.close()
}

}
tvOutput.text = stringBuilder.toString()

private fun fetchSmsMessages() {
val contentResolver: ContentResolver = contentResolver
val uri: Uri = Telephony.Sms.CONTENT_URI
val cursor = contentResolver.query(uri, null, null,
null, null)
val stringBuilder = StringBuilder()
cursor?.let {
while (it.moveToNext()) {
val address = it.getString(it.getColumnIndex(Telephony.Sms.ADDRESS))
val body = it.getString(it.getColumnIndex(Telephony.Sms.BODY))
stringBuilder.append("From: $address\nMessage: $body\n\n")
}
it.close()
}

tvOutput.text = stringBuilder.toString()

}

override fun onRequestPermissionsResult(requestCode: Int,
permissions: Array<out String>, grantResults: IntArray) {
super.onRequestPermissionsResult(requestCode, permissions, grantResults)

}

when (requestCode) {
REQUEST_CONTACTS_PERMISSION -> {
if (grantResults.isNotEmpty() && grantResults[0] ==
PackageManager.PERMISSION_GRANTED)
{
fetchContacts()
}
}
REQUEST_SMS_PERMISSION -> {
if (grantResults.isNotEmpty() && grantResults[0] ==
PackageManager.PERMISSION_GRANTED)
{
fetchSmsMessages()
}
}
}
}

To be added in AndroidManifest.xml
<uses-permission android:name="android.permission.READ_CONTACTS" />
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.READ_EXTERNAL_STORAGE" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE" />

Ex – 06: Broadcast Receivers
activity_main_xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
android:padding="16dp"
android:gravity="center">
<Button
android:id="@+id/btnCheckAirplaneMode"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Check Airplane Mode" />
<TextView
android:id="@+id/tvAirplaneModeStatus"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Airplane Mode: Unknown"
android:layout_marginTop="20dp"
android:textSize="18sp" />
</LinearLayout>

MainActivity.kt
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.content.IntentFilter
import android.os.Bundle
import android.provider.Settings
import android.widget.Button
import android.widget.TextView
import androidx.appcompat.app.AppCompatActivity
class MainActivity : AppCompatActivity() {
private lateinit var tvAirplaneModeStatus: TextView
private lateinit var btnCheckAirplaneMode: Button
private val airplaneModeReceiver = object : BroadcastReceiver() {
override fun onReceive(context: Context, intent: Intent) {
val isAirplaneModeOn = Settings.System.getInt(
context.contentResolver,
Settings.Global.AIRPLANE_MODE_ON, 0
) == 1
tvAirplaneModeStatus.text = if (isAirplaneModeOn) "Airplane Mode: On"
else "Airplane Mode: Off"
}
}
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
tvAirplaneModeStatus = findViewById(R.id.tvAirplaneModeStatus)
btnCheckAirplaneMode = findViewById(R.id.btnCheckAirplaneMode)

btnCheckAirplaneMode.setOnClickListener {
val isAirplaneModeOn = Settings.System.getInt(
contentResolver,
Settings.Global.AIRPLANE_MODE_ON, 0
) == 1
tvAirplaneModeStatus.text = if (isAirplaneModeOn) "Airplane Mode: On"
else "Airplane Mode: Off"
}

}

}

// Register the receiver to listen for changes in airplane mode
val filter = IntentFilter(Intent.ACTION_AIRPLANE_MODE_CHANGED)
registerReceiver(airplaneModeReceiver, filter)

override fun onDestroy() {
super.onDestroy()
// Unregister the receiver to avoid memory leaks
unregisterReceiver(airplaneModeReceiver)
}

ACTION_BATTERY_CHANGED
android provider.Telephony.SMS_RECEIVED
ConnectivityManager.CONNECTIVITY_ACTION

<uses-permission android:name="android.permission.BATTERY_STATS" />
<uses-permission android:name="android.permission.READ_SMS" />
<uses-permission android:name="android.permission.RECEIVE_SMS" />
<uses-permission android:name="android.permission.ACCESS_WIFI_STATE" />
<uses-permission android:name="android.permission.CHANGE_WIFI_STATE" />

Ex – 10: Tab Layout
fragment_tab1.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:gravity="center"
android:orientation="vertical">
<TextView
android:id="@+id/text1"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Text 1"
android:textSize="24sp"/>
</LinearLayout>
fragment_tab2.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:gravity="center"
android:orientation="vertical">
<TextView
android:id="@+id/text2"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Text 2"
android:textSize="24sp"/>
</LinearLayout>
fragment_tab3.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:gravity="center"
android:orientation="vertical">
<TextView
android:id="@+id/text3"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Text 3"
android:textSize="24sp"/>
</LinearLayout>
Fragment1.kt
import androidx.fragment.app.Fragment
class Fragment1 : Fragment(R.layout.fragment_tab1) {
// You can add logic here if needed
}
Fragment2.kt
package com.example.appdevlapprep
import androidx.fragment.app.Fragment
class Fragment2 : Fragment(R.layout.fragment_tab2) {
// You can add logic here if needed
}

Fragment3.kt
package com.example.appdevlapprep
import androidx.fragment.app.Fragment
class Fragment3 : Fragment(R.layout.fragment_tab3) {
// You can add logic here if needed
}

ViewPagerAdapter.kt
import androidx.fragment.app.Fragment
import androidx.fragment.app.FragmentActivity
import androidx.viewpager2.adapter.FragmentStateAdapter
class ViewPagerAdapter(fragmentActivity: FragmentActivity) :
FragmentStateAdapter(fragmentActivity) {
override fun getItemCount(): Int = 3 // Three tabs

}

override fun createFragment(position: Int): Fragment {
return when (position) {
0 -> Fragment1() // Tab 1
1 -> Fragment2() // Tab 2
else -> Fragment3() // Tab 3
}
}

activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<androidx.coordinatorlayout.widget.CoordinatorLayout
xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:app="http://schemas.android.com/apk/res-auto"
xmlns:tools="http://schemas.android.com/tools"
android:layout_width="match_parent"
android:layout_height="match_parent"
tools:context=".MainActivity">
<com.google.android.material.tabs.TabLayout
android:id="@+id/tabLayout"
android:layout_width="match_parent"
android:layout_height="wrap_content"
app:tabMode="fixed"
app:tabGravity="fill" />
<androidx.viewpager2.widget.ViewPager2
android:id="@+id/viewPager"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:layout_below="@id/tabLayout" />
</androidx.coordinatorlayout.widget.CoordinatorLayout>

MainActivity.kt
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.viewpager2.widget.ViewPager2
import com.google.android.material.tabs.TabLayout
import com.google.android.material.tabs.TabLayoutMediator

class MainActivity : AppCompatActivity() {
private lateinit var tabLayout: TabLayout
private lateinit var viewPager: ViewPager2
private lateinit var viewPagerAdapter: ViewPagerAdapter
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
tabLayout = findViewById(R.id.tabLayout)
viewPager = findViewById(R.id.viewPager)
viewPagerAdapter = ViewPagerAdapter(this)
viewPager.adapter = viewPagerAdapter

}

}

// Link TabLayout and ViewPager2
TabLayoutMediator(tabLayout, viewPager) { tab, position ->
tab.text = "Tab ${position + 1}" // Set Tab title
}.attach()

gradle.kts(:app)
dependencies {
implementation("com.google.android.material:material:1.8.0")
implementation("androidx.viewpager2:viewpager2:1.0.0")
implementation("androidx.fragment:fragment-ktx:1.5.6")
}

libs.version.toml
[versions]
viewpager2 = "1.0.0"
fragment_ktx = "1.5.6"
[libraries]
viewpager2 = { module = "androidx.viewpager2:viewpager2", version.ref = "viewpager2" }
fragment_ktx = { module = "androidx.fragment:fragment-ktx", version.ref =
"fragment_ktx" }

Ex – 07: Foreground Services
activity_main.xml
<LinearLayout
xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical">
<VideoView
android:id="@+id/videoView"
android:layout_width="wrap_content"
android:layout_height="263dp" />
<Button
android:id="@+id/startServiceButton"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Start Foreground Service"
android:layout_gravity="center"/>
</LinearLayout>
MainActivity.kt
import android.content.Context
import android.content.IntentFilter
import android.net.Uri
import android.os.Bundle
import androidx.appcompat.app.AppCompatActivity
import androidx.localbroadcastmanager.content.LocalBroadcastManager
import com.example.exp_7.databinding.ActivityMainBinding
class MainActivity : AppCompatActivity() {
private lateinit var binding: ActivityMainBinding
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
binding = ActivityMainBinding.inflate(layoutInflater)
setContentView(binding.root)
binding.startServiceButton.setOnClickListener {
val intent = Intent(this, ForegroundService::class.java)
startService(intent)
}

}

LocalBroadcastManager.getInstance(this)
.registerReceiver(videoReceiver, IntentFilter("PlayVideo"))

private val videoReceiver: BroadcastReceiver = object : BroadcastReceiver() {
override fun onReceive(context: Context?, intent: Intent?) {
val videoUrl = intent?.getStringExtra("video_url")
videoUrl?.let {
binding.videoView.setVideoURI(Uri.parse(it))
binding.videoView.start()
}
}
}

}

}

override fun onDestroy() {
super.onDestroy()
LocalBroadcastManager.getInstance(this).unregisterReceiver(videoReceiver)

ForegroundService.kt
import android.app.*
import android.content.*
import android.graphics.Bitmap
import android.graphics.BitmapFactory
import android.media.MediaPlayer
import android.net.Uri
import android.os.Build
import android.os.Environment
import android.os.IBinder
import android.widget.Toast
import androidx.core.app.NotificationCompat
import androidx.localbroadcastmanager.content.LocalBroadcastManager
import java.io.File
import java.io.FileOutputStream
import java.io.IOException
import java.io.InputStream
import java.util.*
class ForegroundService : Service() {
private val CHANNEL_ID = "ForegroundServiceChannel"
private lateinit var mediaPlayer: MediaPlayer
private val IMAGE_RESOURCE_ID = R.raw.img
override fun onCreate() {
super.onCreate()
createNotificationChannel()

}

mediaPlayer = MediaPlayer()
mediaPlayer.setOnCompletionListener {
stopSelf()
}

override fun onStartCommand(intent: Intent?, flags: Int, startId: Int): Int {
val videoIntent = Intent("PlayVideo")
videoIntent.putExtra("video_url",
"android.resource://${packageName}/raw/videoplayback")
LocalBroadcastManager.getInstance(this).sendBroadcast(videoIntent)
// Load and save the image from raw folder
saveImageToExternalStorage()
// Prepare the notification
val notificationIntent = Intent(this, MainActivity::class.java)
val pendingIntent = PendingIntent.getActivity(this, 0,
notificationIntent, PendingIntent.FLAG_IMMUTABLE)
val notification = NotificationCompat.Builder(this, CHANNEL_ID)
.setContentTitle("Foreground Service")
.setContentText("Saving image to storage")
.setSmallIcon(R.drawable.img)
.setContentIntent(pendingIntent)
.build()

}

startForeground(1, notification)
return START_NOT_STICKY

private fun saveImageToExternalStorage() {
try {
// Open the image file from the raw folder
val inputStream: InputStream = resources.openRawResource(IMAGE_RESOURCE_ID)
val bitmap: Bitmap = BitmapFactory.decodeStream(inputStream)

// Prepare the file path where the image will be saved
val picturesDirectory = Environment.getExternalStoragePublicDirectory
(Environment.DIRECTORY_PICTURES)
val file = File(picturesDirectory, "saved_image_${UUID.randomUUID()}.jpg")
// Write the bitmap to the file
FileOutputStream(file).use { out ->
bitmap.compress(Bitmap.CompressFormat.JPEG, 100, out)
}
// Make the file visible in the MediaStore (so it can be accessed in the
Files app)

val mediaScanIntent = Intent(Intent.ACTION_MEDIA_SCANNER_SCAN_FILE)
val contentUri = Uri.fromFile(file)
mediaScanIntent.data = contentUri
sendBroadcast(mediaScanIntent)
Toast.makeText(this, "Image saved to storage", Toast.LENGTH_SHORT).show()
updateNotification("Image Saved to Storage")

}

} catch (e: Exception) {
Toast.makeText(this, "Failed to save image", Toast.LENGTH_SHORT).show()
updateNotification("Failed to save image")
}

private fun updateNotification(contentText: String) {
val notification = NotificationCompat.Builder(this, CHANNEL_ID)
.setContentTitle("Foreground Service")
.setContentText(contentText)
.setSmallIcon(R.drawable.img)
.build()
startForeground(1, notification)
}
private fun createNotificationChannel() {
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.O) {
val serviceChannel = NotificationChannel(
CHANNEL_ID,
"Foreground Service Channel",
NotificationManager.IMPORTANCE_DEFAULT
)
val manager = getSystemService(NotificationManager::class.java)
manager.createNotificationChannel(serviceChannel)
}
}
override fun onDestroy() {
super.onDestroy()
mediaPlayer.stop() // Ensure the media player stops before the service is
destroyed
mediaPlayer.release() // Properly release resources
}

}

override fun onBind(intent: Intent?): IBinder? {
return null
}

AndroidManifest.xml
<?xml version="1.0" encoding="utf-8"?>
<manifest xmlns:android="http://schemas.android.com/apk/res/android"
xmlns:tools="http://schemas.android.com/tools">
<uses-permission android:name="android.permission.INTERNET" />
<uses-permission android:name="android.permission.WRITE_EXTERNAL_STORAGE"
android:maxSdkVersion="28" />
<uses-permission android:name="android.permission.FOREGROUND_SERVICE" />
<application
android:allowBackup="true"
android:icon="@mipmap/ic_launcher"
android:label="@string/app_name"
android:roundIcon="@mipmap/ic_launcher_round"
android:supportsRtl="true"
android:theme="@style/Theme.Exp_7">
<!-- MainActivity declaration -->
<activity
android:name=".MainActivity"
android:exported="true">
<intent-filter>
<action android:name="android.intent.action.MAIN" />
<category android:name="android.intent.category.LAUNCHER" />
</intent-filter>
</activity>
<!-- ForegroundService declaration -->
<service
android:name=".ForegroundService"
android:enabled="true"
android:exported="false" />
</application>
</manifest>

Ex – 9: Bluetooth Devices Access
activity_main.xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
android:layout_width="match_parent"
android:layout_height="match_parent"
android:orientation="vertical"
android:padding="16dp">
<TextView
android:id="@+id/appTitle"
android:layout_width="wrap_content"
android:layout_height="wrap_content"
android:text="Bluetooth Device Discovery"
android:textSize="24sp"
android:textStyle="bold"
android:layout_gravity="center"
android:paddingBottom="16dp" />
<Button
android:id="@+id/btnDiscover"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:text="Discover Bluetooth Devices" />
<ListView
android:id="@+id/listViewDevices"
android:layout_width="match_parent"
android:layout_height="wrap_content"
android:dividerHeight="1dp" />
</LinearLayout>

MainActivity.kt
import android.Manifest
import android.bluetooth.BluetoothAdapter
import android.bluetooth.BluetoothDevice
import android.content.BroadcastReceiver
import android.content.Context
import android.content.Intent
import android.content.IntentFilter
import android.content.pm.PackageManager
import android.os.Build
import android.os.Bundle
import android.widget.ArrayAdapter
import android.widget.Button
import android.widget.ListView
import android.widget.Toast
import androidx.appcompat.app.AppCompatActivity
import androidx.core.app.ActivityCompat
import androidx.core.content.ContextCompat
class MainActivity : AppCompatActivity() {
private lateinit var bluetoothAdapter: BluetoothAdapter
private lateinit var btnDiscover: Button
private lateinit var listViewDevices: ListView
private lateinit var deviceListAdapter: ArrayAdapter<String>
private val discoveredDevices = mutableListOf<String>()
override fun onCreate(savedInstanceState: Bundle?) {
super.onCreate(savedInstanceState)
setContentView(R.layout.activity_main)
btnDiscover = findViewById(R.id.btnDiscover)
listViewDevices = findViewById(R.id.listViewDevices)

// Initialize BluetoothAdapter
bluetoothAdapter = BluetoothAdapter.getDefaultAdapter()
if (bluetoothAdapter == null) {
Toast.makeText(this, "Bluetooth not supported", Toast.LENGTH_SHORT).show()
return
}
// Set up the ListView adapter
deviceListAdapter = ArrayAdapter(this, android.R.layout.simple_list_item_1,
discoveredDevices)
listViewDevices.adapter = deviceListAdapter
// Set button click listener to show connected devices and start discovery
btnDiscover.setOnClickListener {
showConnectedDevices() // Show already paired devices
startBluetoothDiscovery() // Start discovering nearby devices
}
// Register for broadcasts when a device is discovered and when discovery is
finished
val filter = IntentFilter(BluetoothDevice.ACTION_FOUND)
registerReceiver(receiver, filter)
val filterDiscoveryFinished =
IntentFilter(BluetoothAdapter.ACTION_DISCOVERY_FINISHED)
registerReceiver(receiver, filterDiscoveryFinished)
}
private fun showConnectedDevices() {
discoveredDevices.clear() // Clear the list to refresh with newly connected or
discovered devices
val pairedDevices = bluetoothAdapter.bondedDevices
pairedDevices?.forEach { device ->
val deviceName = device.name ?: "Unknown Device"
val deviceAddress = device.address
val deviceInfo = "$deviceName - $deviceAddress (Connected)"
discoveredDevices.add(deviceInfo)
}
deviceListAdapter.notifyDataSetChanged()
}
private fun startBluetoothDiscovery() {
// Check Bluetooth permissions for Android 12 and higher
if (Build.VERSION.SDK_INT >= Build.VERSION_CODES.S) {
if (ContextCompat.checkSelfPermission(this,
Manifest.permission.BLUETOOTH_SCAN) != PackageManager.PERMISSION_GRANTED ||
ContextCompat.checkSelfPermission(this,
Manifest.permission.BLUETOOTH_CONNECT) != PackageManager.PERMISSION_GRANTED) {
ActivityCompat.requestPermissions(
this,
arrayOf(Manifest.permission.BLUETOOTH_SCAN,
Manifest.permission.BLUETOOTH_CONNECT),
1
)
return
}
} else {
if (ContextCompat.checkSelfPermission(this,
Manifest.permission.ACCESS_FINE_LOCATION) != PackageManager.PERMISSION_GRANTED) {
ActivityCompat.requestPermissions(this,
arrayOf(Manifest.permission.ACCESS_FINE_LOCATION), 1)
return
}
}

}

// Enable Bluetooth if it's not enabled
if (!bluetoothAdapter.isEnabled) {
val enableBtIntent = Intent(BluetoothAdapter.ACTION_REQUEST_ENABLE)
startActivityForResult(enableBtIntent, 1)
} else {
// Start discovery
if (bluetoothAdapter.isDiscovering) {
bluetoothAdapter.cancelDiscovery()
}
bluetoothAdapter.startDiscovery()
Toast.makeText(this, "Starting discovery...", Toast.LENGTH_SHORT).show()
}

// BroadcastReceiver for ACTION_FOUND and ACTION_DISCOVERY_FINISHED
private val receiver = object : BroadcastReceiver() {
override fun onReceive(context: Context, intent: Intent) {
when (intent.action) {
BluetoothDevice.ACTION_FOUND -> {
val device: BluetoothDevice? =
intent.getParcelableExtra(BluetoothDevice.EXTRA_DEVICE)
device?.let {
val deviceName = it.name ?: "Unknown Device"
val deviceAddress = it.address
val deviceInfo = "$deviceName - $deviceAddress"
if (!discoveredDevices.contains(deviceInfo)) {
discoveredDevices.add(deviceInfo)
deviceListAdapter.notifyDataSetChanged()
}
}
}
BluetoothAdapter.ACTION_DISCOVERY_FINISHED -> {
Toast.makeText(context, "Discovery finished",
Toast.LENGTH_SHORT).show()
}
}
}
}

}

override fun onDestroy() {
super.onDestroy()
unregisterReceiver(receiver)
bluetoothAdapter.cancelDiscovery()
}

To be added in Manifest
<uses-permission android:name="android.permission.BLUETOOTH"/>
<uses-permission android:name="android.permission.BLUETOOTH_ADMIN"/>
<uses-permission android:name="android.permission.ACCESS_FINE_LOCATION"/>
<uses-permission android:name="android.permission.ACCESS_COARSE_LOCATION"/>
<uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />
<uses-permission android:name="android.permission.BLUETOOTH_SCAN" />
<uses-permission android:name="android.permission.BLUETOOTH_CONNECT" />


Ex – 10: Swiping
Here’s the complete code for your Android app using `TabLayout` and `ViewPager2` to create a 3-tab swipeable layout. Each tab will display a different fragment: List of Products, Shop Details, and Offers.

### 1. `build.gradle` (Module: app)
Add the necessary dependencies for `TabLayout` and `ViewPager2`.

```gradle
dependencies {
    implementation 'com.google.android.material:material:1.4.0'
    implementation 'androidx.viewpager2:viewpager2:1.0.0'
}
```

### 2. `activity_main.xml`
Create the main layout for `TabLayout` and `ViewPager2`.

```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:orientation="vertical">

    <com.google.android.material.tabs.TabLayout
        android:id="@+id/tab_layout"
        android:layout_width="match_parent"
        android:layout_height="wrap_content" />

    <androidx.viewpager2.widget.ViewPager2
        android:id="@+id/view_pager"
        android:layout_width="match_parent"
        android:layout_height="match_parent" />

</LinearLayout>
```

### 3. Fragment Layouts
Create separate layouts for each fragment.

#### `fragment_products.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="List of Products"
        android:textSize="18sp" />
</LinearLayout>
```

#### `fragment_shop_details.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Shop Details"
        android:textSize="18sp" />
</LinearLayout>
```

#### `fragment_offers.xml`
```xml
<?xml version="1.0" encoding="utf-8"?>
<LinearLayout xmlns:android="http://schemas.android.com/apk/res/android"
    android:layout_width="match_parent"
    android:layout_height="match_parent"
    android:gravity="center"
    android:orientation="vertical">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:text="Offers"
        android:textSize="18sp" />
</LinearLayout>
```

### 4. Fragment Classes
Create a separate fragment class for each tab.

#### `ProductsFragment.java`
```java
package com.example.yourapp;

import android.os.Bundle;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

public class ProductsFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_products, container, false);
    }
}
```

#### `ShopDetailsFragment.java`
```java
package com.example.yourapp;

import android.os.Bundle;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

public class ShopDetailsFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_shop_details, container, false);
    }
}
```

#### `OffersFragment.java`
```java
package com.example.yourapp;

import android.os.Bundle;
import androidx.annotation.NonNull;
import androidx.annotation.Nullable;
import androidx.fragment.app.Fragment;
import android.view.LayoutInflater;
import android.view.View;
import android.view.ViewGroup;

public class OffersFragment extends Fragment {

    @Nullable
    @Override
    public View onCreateView(@NonNull LayoutInflater inflater, @Nullable ViewGroup container, @Nullable Bundle savedInstanceState) {
        return inflater.inflate(R.layout.fragment_offers, container, false);
    }
}
```

### 5. ViewPagerAdapter
Create an adapter to manage the fragments in `ViewPager2`.

#### `ViewPagerAdapter.java`
```java
package com.example.yourapp;

import androidx.annotation.NonNull;
import androidx.fragment.app.Fragment;
import androidx.fragment.app.FragmentActivity;
import androidx.viewpager2.adapter.FragmentStateAdapter;

public class ViewPagerAdapter extends FragmentStateAdapter {

    public ViewPagerAdapter(@NonNull FragmentActivity fragmentActivity) {
        super(fragmentActivity);
    }

    @NonNull
    @Override
    public Fragment createFragment(int position) {
        switch (position) {
            case 0:
                return new ProductsFragment();
            case 1:
                return new ShopDetailsFragment();
            case 2:
                return new OffersFragment();
            default:
                return new ProductsFragment();
        }
    }

    @Override
    public int getItemCount() {
        return 3;
    }
}
```

### 6. MainActivity
In `MainActivity.java`, set up the `TabLayout` and `ViewPager2`.

#### `MainActivity.java`
```java
package com.example.yourapp;

import android.os.Bundle;
import androidx.appcompat.app.AppCompatActivity;
import androidx.viewpager2.widget.ViewPager2;
import com.google.android.material.tabs.TabLayout;
import com.google.android.material.tabs.TabLayoutMediator;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

        TabLayout tabLayout = findViewById(R.id.tab_layout);
        ViewPager2 viewPager = findViewById(R.id.view_pager);

        ViewPagerAdapter adapter = new ViewPagerAdapter(this);
        viewPager.setAdapter(adapter);

        new TabLayoutMediator(tabLayout, viewPager, (tab, position) -> {
            switch (position) {
                case 0:
                    tab.setText("Products");
                    break;
                case 1:
                    tab.setText("Shop Details");
                    break;
                case 2:
                    tab.setText("Offers");
                    break;
            }
        }).attach();
    }
}
```

### Summary
This code creates a 3-tab swipeable layout with `TabLayout` and `ViewPager2`, where each tab displays a different fragment (List of Products, Shop Details, and Offers). Each fragment can be customized further to add specific content or functionality for your app.


