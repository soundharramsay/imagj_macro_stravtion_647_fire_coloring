# imagj_macro_stravtion_647_fire_coloring
imagej_starvation_fire_coloring

halo647 channel >>> 3d projection>>> ltu fire>>save as png


// Define the fixed input directory
inputDir = "/Users/soundhar/Desktop/ben_lab_imac/microscopy/confocal/43_STRAVATION_IDR_STR_DELETIONS_11HRS_12HRS_FBS_STARVED/";

// Get list of all files in the folder
list = getFileList(inputDir);

// Loop through all .czi files
for (i = 0; i < list.length; i++) {
    if (endsWith(list[i], ".czi")) {
        print("Processing: " + list[i]);

        // Open the .czi file
        open(inputDir + list[i]);

        // Store the image title
        imgTitle = getTitle();

        // Optional: wait for stack to load completely
        wait(500);

        // Run 3D Projection
        run("3D Project...", "projection=[Brightest Point] axis=Y-Axis slice=1.01 initial=0 total=360 rotation=10 lower=1 upper=255 opacity=0 surface=100 interior=50");

        // Apply Fire LUT
        run("Fire");

        // Save the projection
        saveAs("PNG", inputDir + "Projections_of_" + replace(imgTitle, ".czi", "") + ".png");

        // Close projection
        close();

        // Close original image
        selectImage(imgTitle);
        close();
    }
}
