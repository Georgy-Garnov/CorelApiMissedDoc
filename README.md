# CorelApiMissedDoc

Target of project is to provide additional documentation for developers of CorelDraw extensions macros and addons.

Concepts that need to be described in more details:

*  Structure of drawui.xml file.

*  Available properties of drawui elements and their possible values.

*  Built in datasources and their properties and methods.

*  CQL Query Language

*  CQL objects associated with document objects and their properties 
*  Cookbook for extending interface of CorelDraw
*  Structure of config.xml files + building and adding binary resources to extension DLL's (strings / icons / cursors)

### List of all DataSource with their properties and methods

Simple php script to build list

```php
<?php
$data = file_get_contents('drawui.xml');
$matches = [];
preg_match_all('/DataSource=([a-zA-Z0-9]+){1,1};Path=([A-Za-z0-9]+)(?:\)|;)/', $data, $matches);
$dses = $matches[1];
$props = $matches[2];
$result = [];
foreach ($dses as $key => $ds) {
   if (!isset($result[$ds])) {
      $result[$ds] = [];
   }
   if (!in_array($props[$key], $result[$ds])) {
      $result[$ds][] = $props[$key];
   }
}
ksort($result);
foreach ($result as $ds => $methods) {
   asort($methods);
   foreach ($methods as $method) {
      echo "$ds => $method \r\n";
   }
}
```

Result:

[List of all DataSource with their properties and methods](./DSList.md)