
### DataLoader Object

DataLoaders: They assemble some data into a suitable format for model training. 
	`DataLoaders` is a thin class that just stores whatever `DataLoader` objects you pass to it, and makes them available as `train` and `valid`. Although it's a very simple class, it's very important in fastai: it provides the data for your model. The key functionality in `DataLoaders` is provided with just these four lines of code (it has some other minor functionality we'll skip over for now):

  

```python

class DataLoaders(GetAttr):

def __init__(self, *loaders): self.loaders = loaders

def __getitem__(self, i): return self.loaders[i]

train,valid = add_props(lambda i,self: self[i])

```

  

To turn data into a `DataLoaders` object we need to tell fastai at least four things:

- What kinds of data we are working with

- How to get the list of items

- How to label these items

- How to create the validation set

Example of creation of data loaders: 
```
bears = DataBlock(

	blocks=(ImageBlock, CategoryBlock),

	get_items=get_image_files,
	
	splitter=RandomSplitter(valid_pct=0.2, seed=42),
	
	get_y=parent_label,
	
	item_tfms=Resize(128)
)

```

once the DataBlock object (a template) is created,we have to tell fastai the actual source of the data

```
dls = bears.dataloaders(path)
```

The DataLoader is a class that provides batches of a few items at a time to the GPU. Fastai's dataloader will give you 64 (by default) items at a time. 




### Learn object
`learn` is an object that contains a model and data. 