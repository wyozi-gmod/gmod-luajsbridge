Lua-JS Bridge for Garry's Mod
=====

Allows easily interacting with DHTML Panel's Javascript from GLua (and hopefully vice versa at some point).

Automatically adds a ```Bridge``` field to newly created DHTML panels, which can be used to call JS functions. You can also call ```luajsbridge.CreateBridge(htmlpnl)``` to create a bridge object.

```lua
local dhtml = vgui.Create("DHTML")
dhtml:SetHTML([[
    <script>
    test = {}
    test.inner = {}
    test.inner.func = function(str, num, obj) {
        console.log("str: " + str);
        console.log("num: " + num);
        console.log("obj.str: " + obj.str);
        console.log("obj.num: " + obj.num);
        console.log("obj.innerTable.key: " + obj.innerTable.key);
    }
    </script>
]])

local bridge = dhtml.Bridge

bridge.test.inner.func("Hello JS", 42, {
    str = "string",
    num = 13,
    innerTable = {
        key = "value"
    }
})

-- Need to give some time for JS to run
timer.Simple(2, function()
    dhtml:Remove()
end)
```
