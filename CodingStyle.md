# Coding style

* This project uses 4 space indentation, not tabs.
* **Class names** are UpperCamelCased
```Cpp
class DigitalSensor : public BaseSensor {
    [...]
}
```
* **Method names** are lowerCamelCased:
```Cpp 
int buttonFromRelay(unsigned int relay_id) {
    [...]
}
```
* **Variables** *should be* underscored_lower_case (I know, I don't always follow this rule myself - in many cases they are also lowerCamelCased):
```Cpp
// Preferred:
bool delete_flag = false;

// Less preferred:
unsigned long rfCodeON = 0;
```
* **Private** methods and variables (even if private to the module they are declared on) are "_"-leaded
```Cpp
bool _dcz_enabled = false;

int _domoticzRelay(unsigned int idx) {
    [...]
}

```
* Function and if() / for() **starting bracket** is in the same line:
```Cpp
int _domoticzRelay(unsigned int idx) {
    [...]
}
 
```

# Linting

Code is checked using cppcheck.

I know current code does not always follow these rules. I'm fixing it as I rework each of the modules.

