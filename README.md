-- Fonction pour vérifier si l'inventaire est plein
local function isInventoryFull()
    for i = 1, 16 do
        if turtle.getItemCount(i) == 0 then
            return false
        end
    end
    return true
end

-- Fonction pour détecter et couper le bois
local function chopWood()
    local success, data = turtle.inspect()
    if success and data.name:find("log") then
        turtle.dig()
        return true
    end
    return false
end

-- Fonction pour contourner les obstacles
local function avoidObstacle()
    turtle.turnRight()
    if not turtle.forward() then
        turtle.dig()
        turtle.forward()
    end
    turtle.turnLeft()
end

-- Fonction principale pour trouver et collecter du bois
local function findWood()
    while true do
        if isInventoryFull() then
            print("Inventaire plein, retour à la base!")
            break
        end

        if not chopWood() then
            -- Si ce n'est pas du bois, contourne l'obstacle
            if not turtle.forward() then
                avoidObstacle()
            end
        else
            -- Avance si le bois a été coupé
            turtle.forward()
        end
    end
end

-- Lancer le programme
print("Début de la recherche de bois...")
findWood()
print("Programme terminé.")
