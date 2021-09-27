//Ask the user to pick the source directory
dir=getDirectory("Select the source directory");

//Generate a (sorted) list of files in the selected directory
list=getFileList(dir);
Array.sort(list);

filename="/Users/Cielo/Desktop/大学课程/ETH/2021-2022/Generation intro to labs/Image analysis/hands_on/plate#1.nd2";
series_num=1
options="open=["+filename+"] split_channels series_"+series_num

//Process all files
for (i=0; i<41;i++){
 run("Bio-Formats Importer", options);
 selectWindow("plate#1.nd2 - plate#1.nd2 (series 01) - C=0");
 run("Grays");
 run("Subtract Background...", "rolling=50");
 setAutoThreshold("Default dark");
 //run("Threshold...");
 setOption("BlackBackground", true);
 run("Convert to Mask");
 run("Erode");
 run("Median...", "radius=2");
 run("Convert to Mask");
 run("Watershed");
 run("Analyze Particles...", "size=50-Infinity summarize");
}