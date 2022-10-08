# ExampleMetadataGameAssetContractERC1155
Metadata according to the example ERC1155 game asset contract. 

This example focuses on the usage in a game. There is no contract URI implemented because I haven't completely explored these mechanics yet. This will follow in a later example.

## Requirements
### Require 00: Metadata workspace connected to your Pinata account

Follow this short example if you need to set it up: https://github.com/MathiasSchneider86/ExampleMetadataIpfsUpload

## Metadata content

For a complete set of metadata you need at first the images, because they will be linked in the tokens metadata (.json file). And that's almost all we need here.

To show the possibilities / the difference of dynamic (upgradeable) and static (fixed) metadata, this example contains a secondary .json file for the game assets in the token contract. This will contain the status values to integrate them later in game. 

So the metadata content is spread in 3 folders:

![ScreenShot](/img/MPD_Structure.PNG)

### _data Folder
For each token id there is a .json file. This is the part of the metadata which is displayed for ecample at opensea. So it is absolutely recommended to follow their actual standards to design such a metadata. 

Important hint at this point: The letters from the hex number in the files name must be lower case, otherwise their might be some problems when trying to watch them on onpensea. Anyway you could even name them in another way if you don't need a public display interface from the marketplaces. You just have to create the correct link from the URI string when querying the files in your application.

### _images Folder
The images are inserted in the metadata as complete link, so you can name the like you want. In this example the enumeration is made decimal to point on that circumstance.

### _stats Folder
The contract contains 11 token ids. The ids 1 to 5 represent the ingame assets which are spread in 5 rarities. So we create 5 .json object files and put some values in there to pick them up later in a game. 

## Uploading the metadata to ipfs
### Upload the images

Navigate to the metadata folder and start the upload process for the images folder:

```
> cd MetadataProtoDice
> pinata-cli -u MPD_images 
Pinning, please wait...
{
  IpfsHash: 'QmP9dXGZ7aKfTW7nPf6SZR8kSEScmQocUGDJ4iw28KNTnf',
  PinSize: 939621,
  Timestamp: '2022-10-08T09:12:00.093Z'
}
```

View in browser should then look like this:

![ScreenShot](/img/ipfs_folder_MPD_images.PNG)

With the returned ipfs hash you can create the image links for the token metadata:

```
https://gateway.pinata.cloud/ipfs/QmP9dXGZ7aKfTW7nPf6SZR8kSEScmQocUGDJ4iw28KNTnf/02_dice_rare.PNG
```

![ScreenShot](/img/ipfs_file_folder_hash_MPD_images.PNG)

It should be mentioned that there is also an unique hash for each of the pictures, so you could also find the file through this link type:

![ScreenShot](/img/ipfs_file_own_hash_MPD_images.PNG)

### Update the .json metadata files and upload them

With this style we put the links in the .json file for each token:

![ScreenShot](/img/metadata_ipfs_link_MPD_images.PNG)

Then comes the upload to ipfs:

```
> pinata-cli -u MPD_data 
Pinning, please wait...
{
  IpfsHash: 'QmZgAKuu8wBR3tMmZrTLC5ARAQoRD1oURDYigjNHJVYD93',
  PinSize: 3792,
  Timestamp: '2022-10-08T10:45:19.177Z'
}
```

View in browser should then look like this:

![ScreenShot](/img/ipfs_folder_MPD_data.PNG)

With the returned ipfs hash you can create the metadata links for each token:

```
https://gateway.pinata.cloud/ipfs/QmZgAKuu8wBR3tMmZrTLC5ARAQoRD1oURDYigjNHJVYD93/0000000000000000000000000000000000000000000000000000000000000002.json
```
![ScreenShot](/img/ipfs_file_MPD_data.PNG)

And with the above link we can determine the token URI as the following:

```
https://gateway.pinata.cloud/ipfs/QmZgAKuu8wBR3tMmZrTLC5ARAQoRD1oURDYigjNHJVYD93/{id}.json
```

In your game or application you can replace {id} with the hex number as string to query the json object.

Further this link will be used in the constructor of the token, so this data is fixed from this point.

### Upload status values

In this case the stats will be uploaded to ipfs, but typically it makes sense to provide them in another way (server containing your static web page hosting for example), because this is flexible and could be updated. 
