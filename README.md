# AC3D
Compressed 3D Model Exporting Format

The AC3D Format add-on for Blender allows you to import and export 3D models using the Advanced Compressed 3D (AC3D) format. This format provides significant file size reduction through compression while maintaining visual quality.

Installation

1-Download the Add-on
2-Download the ac3d_blender_addon.zip file
3-Install in Blender
4-Open Blender and go to Edit > Preferences
5-Select the "Add-ons" tab
6-Click "Install..." button at the top
7-Browse to the downloaded ZIP file and select it
8-Click "Install Add-on"
9-Enable the add-on by checking the box next to "Import-Export: AC3D Format"


Verify Installation
The add-on should now appear in the File > Import and File > Export menus

Exporting Models from Blender

1-Basic Export

Select the objects you want to export
Go to File > Export > AC3D (.ac3d)
Choose where to save your file and set a filename
Configure export options (see below)
Click Export AC3D

2-Export Options

Use Compression: Enable to compress geometry data (recommended)
Error Threshold: Controls the balance between file size and quality

Lower values (0.0001-0.001): High quality, larger files
Medium values (0.001-0.01): Good balance for most models
Higher values (0.01-0.1): Maximum compression, may show visual artifacts


Export Textures: Include texture references in the file
Embed Textures: Store texture data directly in the file
Export Animations: Include animation data in the file

Export Tips

Select appropriate error threshold based on your model's purpose:

Detailed hero assets: 0.0001-0.001
Standard game assets: 0.001-0.01
Background objects: 0.01-0.1

Check the system console (Window > Toggle System Console) for detailed information about compression results
Test your exports by re-importing them to verify quality

Importing AC3D Models

Go to File > Import > AC3D (.ac3d)
Navigate to the AC3D file you want to import
Select the file and click Import AC3D

Import Features

Geometry: All mesh data including vertex positions, normals, UVs
Materials: Both standard and PBR materials are supported
Textures: Referenced textures are linked (if found in the specified path)
Skeletons: Bone structures are imported as Blender armatures
Animations: Animation data is imported as actions
Instances: Multiple instances of the same mesh are imported efficiently

Working with Materials
Standard Materials
Standard Blender materials are exported as traditional materials in AC3D format.
PBR Materials
For best results with PBR workflows:

Use Principled BSDF shader in your materials
Set appropriate values for:

Base Color
Metallic
Roughness
Normal maps
Emission

Texture Maps
The add-on recognizes and exports the following texture maps:

Diffuse/Base Color
Normal
Roughness
Metallic
Ambient Occlusion
Emission

Working with Animations

Exporting Animations
Create keyframe animations on your objects/armatures
Make sure "Export Animations" is enabled in export options
All actions in the Blender file will be exported

Animation Compression

The add-on automatically applies intelligent keyframe reduction to animations, preserving motion quality while reducing file size.
Working with Instances
If you have duplicate objects that share the same mesh data, the add-on will automatically export them as instances, dramatically reducing file size.
Troubleshooting
Common Issues

Missing Textures on Import

Ensure textures are in the path specified in the AC3D file
Or use "Embed Textures" option when exporting

Incorrect Material Appearance

PBR materials require correct mapping of parameters
Check that texture maps are correctly assigned in your material

Export Takes a Long Time

Large models with many vertices may take longer to compress
Try using a higher error threshold to speed up the process

Import Errors

Make sure you're using a valid AC3D file
Check the console for specific error messages

Getting Help
If you encounter issues:

Check the system console for detailed error messages
Verify you're using the latest version of the add-on
Contact support at abdullahasaadghali@gmail.com

Advanced Features

Metadata
The add-on preserves metadata in AC3D files, such as:

Creator information
Creation date
Copyright information
Custom properties

Custom Compression Settings
For advanced users, you can modify the compression algorithms by editing:
python# In ac3d_core/ac3d_compression.py
def compress_mesh(mesh, error_threshold):
    # Customize compression parameters here
Batch Processing
For studios needing to batch process multiple files, the add-on provides:
pythonimport bpy

# Batch export example
def batch_export_ac3d(file_list, output_dir, error_threshold=0.001):
    for file_path in file_list:
        # Load file
        bpy.ops.wm.open_mainfile(filepath=file_path)
        
        # Set output path
        filename = bpy.path.basename(file_path)
        output_path = os.path.join(output_dir, os.path.splitext(filename)[0] + ".ac3d")
        
        # Export as AC3D
        bpy.ops.export_scene.ac3d(
            filepath=output_path,
            use_compression=True,
            error_threshold=error_threshold
        )
        
Best Practices

Organize Your Models

Use clear, consistent naming for objects and materials
Group related objects before export

Prepare Meshes

Clean up geometry before export (remove doubles, etc.)
Apply modifiers when appropriate

UV Mapping

Create clean UV maps for best texture compression
Avoid overlapping UVs if possible

Test Your Results

Always verify exported files by re-importing them
Compare visual quality and file size to find the right balance

Version Control

Store both source .blend files and exported .ac3d files
Document compression settings used for each export

By following this guide, you'll be able to effectively use the AC3D Format add-on to create high-quality, compact 3D models for your projects.
