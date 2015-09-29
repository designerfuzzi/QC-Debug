Debug: Quartz Composer - Mesh Importer

Symptoms in system log: Unknown class 'SCNView', using 'NSView' instead. Encountered in Interface Builder file at path
/System/Library/Frameworks/Quartz.framework/Versions/A/Frameworks/QuartzComposer.framework/Resources/QCCore3DLoaderUI.nib

Talk: This bug is living in Quartz.framework, happens because SCNView class changed but Mesh Importer got no attention refreshing its ViewController to this changes.
Seems there is also a bug while observing KVO output of that SceneView and using -[NSKeyedUnarchiver decodeObjectForKey:]: cannot decode object of class (SCNView)

Workaround/solution: native Mesh Importer is wrapped in a macro patch, its inputs and outputs are published so available to work but does not reach its viewController to trigger the buggy code. That way you can use Inspector when editing QC patches which make use of Mesh Importer.

Destination:
Copy 'Mesh Importer (debug).qtz' into this folder ~/Library/Graphics/Quartz Composer Patches/

Description:
Workaround of Inspectors SCNView bug. 
This patch imports a digital asset exchange (dae) file, without option to extract all separate meshes into a structure.
Note that mesh data is not saved within the composition.