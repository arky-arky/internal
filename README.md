# internal lua docs


## Namespaces
### cheat
* [log](#cheatlog)
* [add_callback](#cheatadd_callback)
* [remove_callbacks](#cheatremove_callbacks)
* [get_local](#cheatget_local)

### net
* [send_packet](#netsend_packet)
* [send_packet_raw](#netsend_packet_raw)

### gui
* [text](#guitext)

## Structs
* [gamepacket](#gamepacket)



# Functions

## gui.text
`void gui.text(string text)`

Add text to the "content" tab

```lua
function render()
  gui.text("123")
end

cheat.add_callback("Gui", render)
```

## net.send_packet_raw
`void send_packet_raw(gamepacket packet)`

Send raw packet

```lua
packet = {}
packet.type = 3
packet.intX = 5
packet.intY = 23
packet.posX = cheat.get_local().pos.x
packet.posY = cheat.get_local().pos.y
packet.intData = 18
net.send_packet_raw(packet)
cheat.log("Punched block at 5,23")
```

## net.send_packet
`void send_packet(int type, string packet)`

Send generic text packet

```lua
cheat.log("Respawning in a second...")
sleep(1000)
net.send_packet(2, "action|respawn")
```

## cheat.log
`void log(string text)`

Log to growtopia's console

```lua
cheat.log("Hello world")
```

## cheat.get_local
`netavatar get_local()`

Returns local player

```lua
cheat.print("My name is: "..cheat.get_local().name")
```

## cheat.add_callback
`void add_callback(string type, function func)`

Add callback / add hook

```lua
function sendpacket(type, packet)
  if packet:find("action|respawn") then
    cheat.log("Respawned")
  end
end

cheat.add_callback("SendPacket", sendpacket)
```

## cheat.remove_callbacks
`void remove_callbacks()`

Remove all callbacks / hooks

```lua
cheat.remove_callbacks()
```


# Structs

## gamepacket
| Type | Name  | Description |
|:-----|:-----:|:------------|
| Number | Type | Packet type |
| Number | Flags | Packet flags |
| Number | intX | Tile X |
| Number | intY | Tile Y |
| Number | posX | World X |
| Number | posY | World Y |
| Number | intData | Packet intData |
| Number | item | Packet item |
| Number | count1 | Packet count1 |
| Number | count2 | Packet count2 |

## netavatar
| Type | Name | Description |
|:-----|:----:|:------------|
| String | name | Player name |
| String | country | Player country |
| Table  | pos | X,Y of player pos |
| Bool | facingLeft | Facing left or not |
