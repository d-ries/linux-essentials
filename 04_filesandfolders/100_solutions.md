# Assignment CH4

## Task 1
Navigate to your home directory

```bash
cd
```

## Task 3
?> <i class="fa-solid fa-circle-info"></i> You'll need this structure in a next Task

In your homedirectory, create the following structure:
`
PXL/Courses/S1/SystemEss
`



```bash
mkdir -p PXL/Courses/S1/SystemEss
```

## Task 4
Create, without leaving your homedirectory, an empty file named `empty` in each folder created in the previous Task

```bash
touch PXL/Courses/S1/SystemEss/empty PXL/Courses/S1/empty PXL/Courses/empy PXL/empty
```

## Task 5
Remove, with just one command, the folder `PXL` with all contents created in the previous Task

```bash
rm -rf PXL
```

## Task 6
Create a new folder "My Pictures". Go into this folder and create, with just one command, these following files:
- Picture1.JPG
- picture2.JPG
- Picture3.jpg
- picture4.jpg

```bash
mkdir My\ Pictures
cd My\ Pictures
touch Picture1.JPG picture2.JPG Picture3.jpg picture4.jpg
```

## Task 7
Rename all files to with the command `rename` so no capitals exist anymore in any of the filenames

```bash
rename 's/P/p' *
rename 's/JPG/jpg' *
```

## Task 8 (Additional)
Make sure you are located in your homedirectory (~). <br/>
Copy all 'files' from this directory into a subdirectory named `backup` in your homefolder.

```bash
cd
mkdir backup
cp  ~/* backup

cp ~/.* backup # Also copy hidden files

```