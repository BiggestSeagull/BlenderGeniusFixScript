# BlenderGeniusFixScript

![image](https://github.com/BiggestSeagull/BlenderGeniusFixScript/assets/127211653/be8715b7-8818-42ac-ac15-78a7e9a20e35)
![image](https://github.com/BiggestSeagull/BlenderGeniusFixScript/assets/127211653/46693fb3-4988-4839-b37a-658bca6efbd9)

![image](https://github.com/BiggestSeagull/BlenderGeniusFixScript/assets/127211653/c9795db0-0704-4336-96fa-5b2358efb6c5)
![image](https://github.com/BiggestSeagull/BlenderGeniusFixScript/assets/127211653/e07f3ffe-cca0-4bae-81c4-98bda87e1c4c)

```

import bpy

def replace_material(bad_mat, good_mat):
    bad_mat.user_remap(good_mat)
    bpy.data.materials.remove(bad_mat)
    
    
def get_duplicate_materials(og_material):
    
    common_name = og_material.name
    
    if common_name[-3:].isnumeric():
        common_name = common_name[:-4]
    
    duplicate_materials = []
    
    for material in bpy.data.materials:
        if material is not og_material:
            name = material.name
            if name[-3:].isnumeric() and name[-4] == ".":
                name = name[:-4]
            
            if name == common_name:
                duplicate_materials.append(material)
    
    text = "{} duplicate materials found"
    print(text.format(len(duplicate_materials)))
    
    return duplicate_materials


def remove_all_duplicate_materials():
    i = 0
    while i < len(bpy.data.materials):
        
        og_material = bpy.data.materials[i]
        
        print("og material: " + og_material.name)
        
        # get duplicate materials
        duplicate_materials = get_duplicate_materials(og_material)
        
        # replace all duplicates
        for duplicate_material in duplicate_materials:
            replace_material(duplicate_material, og_material)
        
        # adjust name to no trailing numbers
        if og_material.name[-3:].isnumeric() and og_material.name[-4] == ".":
            og_material.name = og_material.name[:-4]
            
        i = i+1
    

remove_all_duplicate_materials()

```
