import time

from mcpi.minecraft import Minecraft
from mcpi.vec3 import Vec3
import mcpi.block as block

directions = (
    (0, 0, 0),
    (1, 0, 0),
    (1, 0, 1),
    (0, 0, 1),
    (-1, 0, 1),
    (-1, 0, 0),
    (-1, 0, -1),
    (0, 0, -1),
    (1, 0, -1)
)
mc = Minecraft.create()
create_block_positions = []
while True:
    position = mc.player.getTilePos() + Vec3(0, -1, 0)
    new_positions = []
    for direction in directions:
        new_position = position + Vec3(*directions)
        new_positions.append(new_position)
        block_type_id = mc.getBlock(new_position)
        if block_type_id == block.AIR.id:
            mc.setBlock(new_position, block.GLASS)
            create_block_positions.append(new_position)

        for create_block_position in create_block_positions:
            if create_block_position not in new_positions:
                mc.setBlock(create_block_position, block.AIR)

    time.sleep(0.016)
