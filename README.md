# Android-practice-3-SharedPreferences
Preserving data through SharedPreferences interface 

![Alt Text](https://github.com/RobinKim-SWEngineer/Images-for-document/blob/master/sharedPreferences.gif)

In the previous practice `onSaveInstanceState(Bundle outState)` was used to preserve instance state when an activity is destroyed. But there are some cases that this method **is not called** even though the activity is destroyed, for example when user navigates back to earlier activity using back button in action bar.

In such case we can use **SharedPreferences**. It is an interface whose object points to a preference file containing dictionary form of key-value pairs where we can write and read. When writing, we use **SharedPreferences.Editor** which is nested interface.

> For large amount or complex relational data, `SQLite` will be needed. But when it is a small amount of data like flags, ints, booleans etc, **SharedPreferences** fits better since we don't need to write legnthy codes and supporing classes for using SQLite.  

## Related methods
 - To get SharedPreferences instance, use either `Context.getSharedPreferences(String name, int mode)` or `Activity.getPreferences(int mode)`. First method gets us multiple shared preferences objects identified by name. In case of second method, we don't need to supply the name since it returns a default shared preference object that belongs (private) to the activity.
   ```
   SharedPreferences sharedPreferences = getSharedPreferences(name: "orderPreferences", MODE_PRIVATE);
   ```
 - When writing (saving) to shared preferences files, we do through **SharedPreferences.Editor** which we get via `edit()`. Later it is followed by puttings method and `apply()`.
   ```
   SharedPreferences.Editor editor = sharedPreferences.edit();
   editor.putString("previous_order", textViewOrderList.getText().toString());
   editor.apply();
   ```
   > Good place to do this process would be inside `onOptionsItemSelected(MenuItem item) {...}`, which is called when an item in options menu is selected. So if we click the arrow button to **navigate back** to the previous activity, the data will be saved into shared preferences file that we will be able to read from later on.
   
   
 - When reading, we first get shared preferences instance, and call get methods upon it.
   ```
   SharedPreferences sharedPreferences = getSharedPreferences(name: "orderPreferences", MODE_PRIVATE);
   return sharedPreferences.getString("previous_order", defaultStringForPreferenceFile);
   ```
   
 - We can clear the data in the file by `editor.clear()`, which needs to be followed by again, `editor.apply()`.

For more detail implementation of **SharedPreferences** for each step please refer to the attached example.
