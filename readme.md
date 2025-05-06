<p align="center">
    <h1 align="center">Hi 👋, I'm MaDHouSe</h1>
    <h3 align="center">A passionate allround developer </h3>    
</p>

<p align="center">
    <a href="https://github.com/MH-Scripts/mh-vehiclekeyitem/issues">
        <img src="https://img.shields.io/github/issues/MH-Scripts/mh-vehiclekeyitem"/> 
    </a>
    <a href="https://github.com/MH-Scripts/mh-vehiclekeyitem/watchers">
        <img src="https://img.shields.io/github/watchers/MH-Scripts/mh-vehiclekeyitem"/> 
    </a> 
    <a href="https://github.com/MH-Scripts/mh-vehiclekeyitem/network/members">
        <img src="https://img.shields.io/github/forks/MH-Scripts/mh-vehiclekeyitem"/> 
    </a>  
    <a href="https://github.com/MH-Scripts/mh-vehiclekeyitem/stargazers">
        <img src="https://img.shields.io/github/stars/MH-Scripts/mh-vehiclekeyitem?color=white"/> 
    </a>
    <a href="https://github.com/MH-Scripts/mh-vehiclekeyitem/blob/main/LICENSE">
        <img src="https://img.shields.io/github/license/MH-Scripts/mh-vehiclekeyitem?color=black"/> 
    </a>      
</p>

# My Youtube Channel
- [Subscribe](https://www.youtube.com/@MaDHouSe79) 

# MH Vehicle Key Item
- One of the best vehicle key item script for qbcore.

# Dependencies:
- [qb-core](https://github.com/qbcore-framework/qb-core)
- [qb-inventory](https://github.com/qbcore-framework/qb-inventory) 2.0
- [qb-vehiclekeys](https://github.com/qbcore-framework/qb-vehiclekeys) 

# Installation:
- Create a folder `[mh]` in `resources`. 
- Put `mh-vehiclekeyitem` in to `resources/[mh]`.
- Add the vehiclekey image in your inventory image folder.
- Load this script after target and polyzone.
- in sever.sfg after `[standalone]` add -> `ensure [mh]`
- After you done with the instructions below, you can restart the server.

# Key Image
![alttext](https://github.com/MH-Scripts/mh-vehiclekeyitem/blob/main/vehiclekey.png)

# QBCore Shared Item
```lua
vehiclekey = { name = 'vehiclekey', label = 'Vehicle Key', weight = 500, type = 'item', image = 'vehiclekey.png', unique = true, useable = true, shouldClose = true, description = 'A vehicle key.' },
```

# Edit Code in qb-vehiclekeys
- i also recommend using [mh-databaseoptimizer](https://github.com/MH-Scripts/mh-databaseoptimizer) if you use qb-vehiclekeys
- cause if you don;t use that it can happen dat you have a key from other players so use [mh-databaseoptimizer](https://github.com/MH-Scripts/mh-databaseoptimizer) and it does not happends.
- in `qb-vehiclekeys/server/main.lua` around line 77
```lua
function GiveKeys(id, plate)
    local Player = QBCore.Functions.GetPlayer(id)
    if not Player then return end
    local citizenid = Player.PlayerData.citizenid

    if not plate then
        if GetVehiclePedIsIn(GetPlayerPed(id), false) ~= 0 then
            plate = QBCore.Shared.Trim(GetVehicleNumberPlateText(GetVehiclePedIsIn(GetPlayerPed(id), false)))
        else
            return
        end
    end

    if not VehicleList[plate] then VehicleList[plate] = {} end
    VehicleList[plate][citizenid] = true

    exports['mh-vehiclekeyitem']:AddItem(id, plate) -- mh-vehiclekeyitem add here

    TriggerClientEvent('QBCore:Notify', id, Lang:t('notify.vgetkeys'))
    TriggerClientEvent('qb-vehiclekeys:client:AddKeys', id, plate)
    TriggerClientEvent('qb-vehiclekeys:client:GiveKeyItem', id, plate)
end
```

- Although this function below is not used anywhere in qb, but add it just in case they suddenly use it.
```lua
function RemoveKeys(id, plate)
    local Player = QBCore.Functions.GetPlayer(id)
    if not Player then return end
    local citizenid = Player.PlayerData.citizenid

    if VehicleList[plate] and VehicleList[plate][citizenid] then
        VehicleList[plate][citizenid] = nil
    end
    
    exports['mh-vehiclekeyitem']:RemoveItem(id, plate) -- mh-vehiclekeyitem add here
    
    TriggerClientEvent('qb-vehiclekeys:client:RemoveKeys', id, plate)
end
```

# LICENSE
[GPL LICENSE](./LICENSE)<br />
&copy; [MaDHouSe79](https://www.youtube.com/@MaDHouSe79)
