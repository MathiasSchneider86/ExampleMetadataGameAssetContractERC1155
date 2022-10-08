# ExampleMetadataGameAssetContractERC1155
Metadata according to the example ERC1155 game asset contract

## Requirements
### Require 00: Metadata workspace connected to your Pinata account

Follow this short example if you need to set it up: https://github.com/MathiasSchneider86/ExampleMetadataIpfsUpload

## Metadata content

For a complete set of metadata you need at first the images, because they will be linked in the tokens metadata (.json file). And that's almost all we need here.

To show the possibilities / the difference of dynamic (upgradeable) and static (fixed) metadata, this example contains a secondary .json file for the game assets in the token contract. This will contain the status values to integrate them later in game. The idea behind is 

So the metadata content is spread in 3 folders:

![ScreenShot](/img/MPD_Structure.PNG)

### _data Folder
For each token id there is a .json file. This is the part of the metadata which is displayed for ecample at opensea. So it is absolutely recommended to follow their actual standards to design such a metadata.

Important hint at this point: The letters from the hex number in the files name must be lower case, otherwise their might be some problems when trying to watch them on onpensea. Anyway you could even name them in another way if you don't need a public display interface from the marketplaces. You just have to create the correct link from the URI string when querying the files in your application.

### _images Folder
The images are inserted in the metadata as complete link, so you can name the like you want. In this example the enumeration is made decimal to point on that circumstance.

### _stats Folder
The contract contains 11 token ids. The ids 1 to 5 represent the ingame assets which are spread in 5 rarities. So we create 5 .json object files and put some values in there to pick them up later in a game. 
