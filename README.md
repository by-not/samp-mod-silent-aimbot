# Silent Aimbot v1.0 - Features Documentation

## 📋 Overview
Silent Aimbot is an advanced targeting system for SA-MP that provides precise aiming assistance with multiple protection and customization features.

---

## 🎯 Core Features

### **Automatic Target Acquisition**
- Automatically detects and locks onto the nearest target within the configured radius
- Prioritizes targets based on distance to crosshair
- Real-time bone position tracking for accurate hit registration
- Support for 50 different bone points across the body

### **Visual Indicators**
- **Circular Crosshair**: Displays targeting radius around your crosshair
- **Color-Coded System**:
  - 🟢 **Green**: Target visible and in range
  - 🟡 **Yellow**: Target in vehicle
  - 🔴 **Red**: Target behind wall/obstacle

---

## ⚙️ Configuration Sections

### **[Enabled]**
Controls activation and keybinds

#### `AutoActivation`
- **Values**: `0` (Off) / `1` (On)
- **Description**: Automatically enables the aimbot when the script loads
- **Default**: `1`

#### `GameKey`
- **Values**: Virtual Key Codes (hex)
- **Description**: Key to toggle aimbot on/off during gameplay
- **Default**: `0x72` (F3 key)
- **Common Keys**:
  - `0x72` = F3
  - `0x73` = F4
  - `0x74` = F5
  - `0x00` = Disabled (command only)

---

### **[Config]**
Main targeting and behavior settings

#### `HookDistance`
- **Values**: `1` - `999` (pixels)
- **Description**: Radius of the targeting circle around your crosshair
- **Default**: `50`
- **Recommendation**: 
  - Close combat: 30-50
  - Medium range: 50-80
  - Long range: 80-150

#### `IgnoreDistance`
- **Values**: `0` (Off) / `1` (On)
- **Description**: 
  - `0` = Respects weapon's maximum effective range
  - `1` = Ignores distance limits, targets anyone in circle
- **Default**: `0`
- **Note**: Turning this ON may look suspicious

#### `WallShot`
- **Values**: `0` (Off) / `1` (On)
- **Description**: 
  - `0` = Only targets visible enemies
  - `1` = Can shoot through walls/obstacles
- **Default**: `0`
- **⚠️ Warning**: Enabling this is highly detectable

---

### **[Protect]**
Anti-detection and legitimacy features

#### `ModelGroup`
- **Values**: `0` - `8`
- **Description**: Prevents shooting specific gang/faction members
- **Default**: `0` (Disabled)
- **Groups**:
  - `0` = No protection (shoot everyone)
  - `1` = Grove Street Families (105, 106, 107)
  - `2` = Ballas Gang (102, 103, 104)
  - `3` = Aztecas (114, 115, 116)
  - `4` = Los Santos Vagos (108, 109, 110)
  - `5` = San Fierro Rifa (173, 174, 175)
  - `6` = Russian Mafia (111, 112, 125, 126, 127)
  - `7` = La Cosa Nostra (113, 124)
  - `8` = Yakuza/Triads (121, 122, 123, 117, 118, 120)
- **Feature**: Shows "Fuego amigo" (Friendly fire) warning when aiming at protected models

#### `HitRate`
- **Values**: `0` - `100` (percentage)
- **Description**: Accuracy percentage for shot success
- **Default**: `35` (35% accuracy)
- **Examples**:
  - `0` = Never hit (0%)
  - `25` = Very low accuracy (25%)
  - `50` = Half shots hit (50%)
  - `75` = High accuracy (75%)
  - `100` = Perfect aim (100%)
- **🎯 Recommended**: 30-60 for realistic gameplay
- **Purpose**: Makes your aim look more human and less like a bot

---

### **[Sync]**
Network packet modification settings

#### `WeaponsUpdate`
- **Values**: `0` (Off) / `1` (On)
- **Description**: Modifies weapon update packets to include target information
- **Default**: `1`
- **Technical**: Updates PACKET_WEAPONS_UPDATE with target player ID

#### `SendRPC`
- **Values**: `0` (Off) / `1` (On)
- **Description**: Sends damage RPC calls to the server
- **Default**: `1`
- **Technical**: Handles RPC_GIVETAKEDAMAGE communication

#### `AimSync`
- **Values**: `0` (Off) / `1` (On)
- **Description**: Synchronizes camera aim data with target position
- **Default**: `1`
- **Technical**: Modifies PACKET_AIM_SYNC data stream

---

### **[Misc]**
Visual and notification settings

#### `ShowMessages`
- **Values**: `0` (Off) / `1` (On)
- **Description**: Displays on-screen notifications for aimbot status
- **Default**: `1`
- **Messages**:
  - "Silent AIM Activated" (green)
  - "Silent AIM Deactivated" (red)

#### `DrawBlood`
- **Values**: `0` (Off) / `1` (On)
- **Description**: Creates blood effects when hitting targets
- **Default**: `1`
- **Visual**: Adds realistic blood splatter at hit location

#### `BloodDensity`
- **Values**: `1` - `255`
- **Description**: Amount of blood particles generated per hit
- **Default**: `120`
- **Range**:
  - Low: 20-60 (minimal blood)
  - Medium: 80-120 (normal)
  - High: 150-200 (heavy bleeding)

---

## 🎮 Commands

### `/master`
- **Function**: Toggles aimbot on/off
- **Feedback**: Shows activation message if ShowMessages is enabled

### `/recfg`
- **Function**: Reloads configuration from INI file without restarting
- **Feedback**: 
  - Success: "Config file was successfully Reloaded"
  - Error: "Error! Config file doesn't exist!"
- **Use Case**: Change settings in INI and reload without reconnecting

---

## 🔧 Technical Details

### **Bone Targeting System**
The aimbot tracks 50 different bone positions organized by body parts:
- **Head** (8 bones): Maximum damage, smallest target
- **Torso** (6 bones): Medium damage, medium target
- **Arms** (20 bones): Low damage, moving targets
- **Legs** (16 bones): Low damage, large target

### **Damage Calculation**
Weapon damage is automatically calculated based on SA-MP standards:
- **Sniper Rifle**: 41.25 damage
- **Combat Shotgun**: 49.50 damage
- **Desert Eagle**: 46.20 damage
- **M4/AK-47**: 9.90 damage
- And more...

### **Targeting Priority**
1. Distance to crosshair (closest to center)
2. Visibility check (if WallShot is OFF)
3. Range validation (if IgnoreDistance is OFF)
4. Model group protection check

---

## ⚠️ Recommendations

### **Legitimate Settings** (Hard to detect)
```ini
HookDistance=40
IgnoreDistance=0
WallShot=0
HitRate=45
DrawBlood=1
```

### **Aggressive Settings** (Higher detection risk)
```ini
HookDistance=100
IgnoreDistance=1
WallShot=1
HitRate=85
DrawBlood=1
```

### **Stealth Settings** (Maximum legitimacy)
```ini
HookDistance=30
IgnoreDistance=0
WallShot=0
HitRate=35
ModelGroup=[Your Gang]
DrawBlood=1
```

---

## 📝 Notes

- **Performance**: The script runs efficiently with minimal FPS impact
- **Compatibility**: Works with SA-MP 0.3.7 and SAMPFUNCS
- **Updates**: Use `/recfg` to reload settings without restarting
- **Protection**: HitRate feature makes your aim look more human
- **Safety**: Model group protection prevents accidental friendly fire

---

## 🎯 Best Practices

1. **Start Conservative**: Begin with low HitRate (30-40%) and small HookDistance (30-50)
2. **Test Settings**: Use `/recfg` to adjust and test different configurations
3. **Watch Behavior**: Monitor if your aiming looks natural to other players
4. **Use Protection**: Enable ModelGroup if you're in a gang/faction
5. **Stay Updated**: Keep WallShot OFF unless absolutely necessary

---

**Created By**: not  
**Version**: 1.0  
**Support**: For issues or suggestions, contact the developer