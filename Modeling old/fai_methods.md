
- Load Images: `get_image_files(path)`
	This function takes a path, and returns a list of all of the images in that path (recursively by default):
- Verify images to search for corrupt ones
	`fns = get_image_files(path)`
	`verify_images(fns)`

- Remove all failed images:  `failed.map(Path.unlink);`
	To remove all the failed images, you can use `unlink` on each of them. Note that, like most fastai functions that return a collection, `verify_images` returns an object of type `L`, which includes the `map` method. This calls the passed function on each element of the collection:

- Split data into training and validation: `RandomSplitter(valid_pct, seed)`

- Get name of the folder the file is in (so as to get labels for example): `parent_label()`


- Item Transforms: pieces of code that run on each individual item (e.g., image, category, etc.). e.g. (`Resize(size)`) 
  `Resize` crops the images to fit a square shape of the image size requested. But this can result in losing some important details. Use `RandomResizedCrop(size, min_scale = 0.3)` instead

- Take a look at some items of a fastai DataLoader. 
	(if 'dls' is a DataBlock.dataloaders(path))
	```
	dls.valid.show_batch(max_n, nrows)
	```

- Apply a standard set of image data augmentations: `aug_transform(mult)`

- 'cnn_learner' also has a parameter 'pretrained', which defaults to True.



- Train a fastai model from scratch (i.e., without transfer learning) `fit_one_cicle`


- Show images  with the highest loss in the dataset `plot_top_losses`
