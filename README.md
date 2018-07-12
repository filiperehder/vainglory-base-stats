# Vainglory Base Stats v3.4.1.2
A JSON object master file, hard-coded from the game itself, for use in web-based applications that can parse JSON data. Updated for VainGlory patch 3.3!

______________________

## Table of Contents
-  [Getting Started](#getting-started)
-  [Top-Level Data Objects](#top-level-data-objects)
-  [Accessing the Data (as a JavaScript object)](#accessing-the-data-as-a-javascript-object)
-  [Accessing the Data (with an Asynchronous call)](#accessing-the-data-with-an-asynchronous-call)
-  [Data Structure](#data-structure)
-  [Image Files](#image-files)
-  [Road Map](#road-map)
-  [Recent Changes](#road-map)

______________________

### Getting Started
Start by downloading the file, the project zip, or simply copy/paste the data directly into a file for your project.

### Top-Level Data Objects
Within the main Vainglory JSON object, there are currently 2 usable top-level data objects. The data for all of the heroes in the game can be accessed by using the JSON key `heroes`. The data for all of the items can be accessed by using the JSON key `items`.

### Accessing the Data (as a JavaScript object)
If you are using JavaScript, you can simply define the entire `vainglory.json` object as a value for a `var` or `const`, and avoid having to parse the data entirely.
```javascript
const vaingloryObject = {
    "items" : {...},
    "heroes" : {...}
};
```
With this method you can access the data like so:
```javascript
console.log(vaingloryObject.items.aegis.name);  // RETURNS: "Aegis"
console.log(vaingloryObject.heroes.adagio.name);  // RETURNS: "Adagio"
```

### Accessing the Data (with an Asynchronous call)
Many developers would prefer to call a file of this size asynchronously to better manage the UX and load times of their applications. To use this method, you would want to store the data as a file on your server, and use a server-side call to get the data and work with it.

##### If you're using jQuery in your project, you can call the data like so:
```javascript
// jQuery example of heroes key in use

var vainglory;
var vgGit = "data/vainglory.json";

var vgData = $.getJSON( vgGit, function(data) {
    
    vainglory = data;
    
});

// Access data like so:
console.log('Number of Heroes: ' + vainglory.heroes.length);
console.log('Number of Items: ' + vainglory.items.length);
```

##### If you're using standard JavaScript:
```javascript
// Pure JavaScript example of heroes key in use

const vainglory;
const vgGit = "data/vainglory.json";

const request = new XMLHttpRequest();
 
request.onreadystatechange = function() {
  
  if(request.readyState === 4) {
    
    if(request.status === 200) { 
      
      vainglory = request.responseText;
      
      // Access data like so:
      console.log('Number of Heroes: ' + vainglory.heroes.length);
      console.log('Number of Items: ' + vainglory.items.length);
      
    } else {
      
      console.log('An error occurred during your request: ' +  request.status + ' ' + request.statusText);
      
    }
    
  }
  
}
 
request.open('GET', vgGit);
```

### Data Structure
The structure of the JSON data in the vainglory.json file is as follows:
* items
  * item key
    * name
    * thumb
    * category
    * tier
    * cost
    * activate
    * passive
    * vampirism
    * bookofeulogies
    * armorbreaker
    * shieldbreaker
    * cosume
    * boots
    * travelboots
    * stormguard
    * breadth
    * depth
    * stats
      * health
        * value
        * name
        * units
      * health_recharge (same as health)
      * energy (same as health)
      * weapon_power (same as health)
      * crystal_power (same as health)
      * attack_speed (same as health)
      * armor (same as health)
      * shield (same as health)
      * range (same as health)
      * move_speed (same as health)
      * energy_recharge (same as health)
      * cooldown (same as health)
      * crit_chance (same as health)
      * crit_damage (same as health)
      * armor_pierce (same as health)
      * shield_pierce (same as health)
      * weapon_lifesteal (same as health)
      * crystal_lifesteal (same as health)
    * tip
    * build_from
    * build_to
* heroes
  * hero key
    * name
    * thumb
    * difficulty
    * attack_type
    * description
    * primary_role
    * ratings
      * offense
      * defense
      * team_utility
      * mobility
    * stats
      * health
        * name
        * units
        * min
        * max
      * health_recharge (same as health)
      * weapon_power
        * name
        * units
        * wp_scaling
        * min
        * max 
      * crystal_power
        * name
        * units
        * cp_scaling
        * min
        * max 
      * attack_speed (same as health)
      * armor (same as health)
      * shield (same as health)
      * energy (same as health)
      * energy_recharge (same as health)
      * cooldown
        * name
        * units
        * min
      * range (same as cooldown)
      * move_speed (same as cooldown)
      * crit_chance (same as cooldown)
      * crit_damage (same as cooldown)
      * armor_pierce (same as cooldown)
      * shield_pierce (same as cooldown)
      * weapon_lifesteal (same as cooldown)
      * crystal_lifesteal (same as cooldown)
    * abilities
      * heroic_perk
        * name
        * thumb
        * description
        * stat_levels
        * stats (currently false in all cases, but this is the object planned for future inclusion of calculatable stats for perk abilities)
      * a_ability
        * name
        * thumb
        * description
        * stat_levels
        * stats (same for each stat)
          * name
          * values
          * ratios
          * overdrive
      * a_alt (currently for Malene only)
        * name
        * thumb
        * description
        * stat_levels
        * stats (same for each stat)
          * name
          * values
          * ratios
          * overdrive
      * b_ability
        * name
        * thumb
        * description
        * stat_levels
        * stats (same for each stat)
          * name
          * values
          * ratios
          * overdrive
      * b_alt (currently for Malene only)
        * name
        * thumb
        * description
        * stat_levels
        * stats (same for each stat)
          * name
          * values
          * ratios
          * overdrive
      * c_ability
        * name
        * thumb
        * description
        * stat_levels
        * stats (same for each stat)
          * name
          * values
          * ratios
          * overdrive

### Image Files
The link below will provide you with a .zip file from a public dropbox directory. This .zip file has each image thumbnail referenced in the JSON data for each hero, each hero ability and each item. The organization of the image directories are as follows:
  * images
    * abilities
        * [directory with each heroes name]
    * heroes
    * items

<a href="https://www.dropbox.com/s/cdnycug24mx36al/images-vainglory-patch-3-5.zip?dl=0" target="_blank">Download Images Zip</a>

### Road Map
Here are the tasks planned for the future of this project:
1. Add in talent data for each hero

### Recent Changes
Here are the changes from the most recent release:
  * updated all captain hero recommended builds (Adagio, Ardan, Catherine, Churnwalker, Flicker, Fortress, Grace, Lance, Lorelai, Lyra, Phinn)
  * updated alpha's cp recommended build
  * updated glaive's captain recommended build
  * NOTE: grumpjaw's support build is missing the clockwork item in-game! :(
  * updated joule's weapon recommended build
  * updated ozo's crystal recommended build
  * updated taka's weapon recommended build
  * updated taka's glass cannon crystal recommended build
  * updated tony's support recommended build
  * removed reims's double ult (echo) recommended build
  * updated baptiste's support recommended build
  * updated baron's continuous damage recommended build
  * updated baron's artillery crystal recommended build
  * updated blackfeather's poke crystal recommended build
  * updated celeste's continuous damage recommended build
  * updated celeste's Glass Cannon recommended build
  * updated kensei's Continuous Damage recommended build
  * updated kestrel's Deadly Sniper recommended build
  * updated kestrel's Splash Damage recommended build
  * updated kestrel's Stealth Assassin recommended build
  * updated reza's Assassin recommended build
  * updated ringo's Continuous Damage recommended build
  * updated ringo's Burst Damage recommended build
  * updated samuel's Artillery recommended build
  * updated skaarf's Continuous Damage recommended build
  * updated skaarf's Burst Damage recommended build
