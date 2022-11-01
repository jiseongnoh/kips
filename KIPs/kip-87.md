---
kip: 87
title: NFT Avatar Standard
author: Yeri Lee <yeriel.lee@krustuniverse.com>, Junghyun Colin Kim <colin.klaytn@krustuniverse.com>, Wonbae Kim <kernys@supercat.co.kr>, Seokrin Sung <seokrin.sung@supercat.co.kr>
discussions-to:  
status: Draft
type: Standards Track
category: Application
created: 2022-11-01
requires: ERC-721, ERC-1155, KIP-17, KIP-37
---

## Simple Summary
Creating an NFT avatar standard to provide an interchangeable visualization of NFT across multiple metaverses  

## Abstract
Although fungible tokens (FTs) are easily exchangeable across different platforms through DEX, non-fungible tokens (NFTs) do not easily migrate from one metaverse to another. The exchange of NFTs across platforms often does not promise the equivalent asset value, including quality and style. We aim to define an NFT as a single character with different visualization for multi-metaverse. An NFT character with the standard definition and predefined motion images can create an adequate visualization when entering metaverses as an NFT avatar. The NFT avatar standard will increase the utility of NFT, invigorate the metaverse industry and strengthen interoperability. 

## Motivation
NFT has different utilities. Some are used as an asset in the gaming industry while some are used as a parcel of virtual land in the metaverse. The usage of NFTs has often been limited to PFP (profile picture) until today. Yet, an NFT character should be interchanged into several forms of avatars corresponding to the metaverse platform it enters. This standard distinguishes the usage between NFT characters as absolute graphical assets and NFT avatars as motion-added chameleon-ed NFT characters. 

With the NFT avatar standard, NFT characters will transfer into avatars enabling use cases within multiple metaverses. The character purchased in the NFT marketplace can enter as a 2D avatar in Zep.us while it enters Another.world as a 3D avatar. In addition, user-created 3D avatars, like VR Chat, can also compatibly enter multi-metaverse as NFT avatars. 

The NFT avatar standard will generate a positive value creation cycle between creators, the NFT marketplace, and the metaverse. Each individual entity will have a common standard to share, maximizing the utility and interoperability of NFTs. With the standard, the value of an item minted by creators will be increased with heightened practicality and utilization. This will boost the activity within NFT marketplaces while the usage of NFT within metaverses also increases. The versatile utility of NFT characters will increase the public desire to purchase and incentivize creators to generate, ultimately vitalizing the creator economy. Likewise, such dynamics will unleash NFT characters in the multi-metaverse. 

## Specification
The keywords “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY” and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

NFT metadata structured by the official ERC721 metadata standard or the Enjin Metadata suggestions are as follows referring to OpenSea docs.

```JSON Schema
{
  "description": "Friendly OpenSea Creature that enjoys long swims in the ocean.", 
  "external_url": "https://openseacreatures.io/3", 
  "image": "https://storage.googleapis.com/opensea-prod.appspot.com/puffs/3.png", 
  "name": "Dave Starbelly",
  "attributes": { ... }, 
}
```

In addition to the existing NFT metadata standard, the NFT avatar standard supplements the “avatars” section. The data required for the avatar varies by metaverse platform. In the instance of Zep, image URL and animation behavior are defined to maximize the scalability of individual NFT. This standard represents a metadata extension of ERC721.

```JSON Schema
{
  "description": "Friendly OpenSea Creature that enjoys long swims in the ocean.", 
  "external_url": "https://openseacreatures.io/3", 
  "image": "https://storage.googleapis.com/opensea-prod.appspot.com/puffs/3.png", 
  "name": "Dave Starbelly",
  "attributes": [ ... ], 
  "avatars": { ... },
}
```

Each property, corresponding to ERC-721, is defined as below. 
| Variable | Description |
| ----------- | ----------- |
| name | The name of the item. |
| description | A description of the item. |
| external_url | An external URL that will appear below the asset's image. |
| image | An URL to the image of the item. This can be any type of image, including SVG, PNG, IPFS URL, or paths. The recommended size of an image is a width between 320 and 1080 pixels and an aspect ratio between 1.91:1 and 4:5 inclusive. |
| attributes | An attribute for the item, which will show up on the NFT marketplace. |
| avatars | A metaverse platform where the item can be integrated as NFT avatars. | 

Under “avatars,” metadata keys for any metaverse platform, such as Zep.us and Another.world, can be added. The value included in the key will define the animation of a character.  

```JSON Schema
...
{
   "avatars": {
         "zep": {...},
         "another.world": {...},
}
```

This proposal currently only includes the standard of Zep NFT avatars, but the standard of additional services can be also defined under “avatars”. 

```JSON Schema
{
  "zep": {  
             "image": "IMAGE URL",
             "frame_width": 48,
             "frame_height": 64,
"animations": {...}
}
```

Each property is defined as below. 
| Variable | Description |
| ----------- | ----------- |
| zep | The key defined by zep.us |
| image | A URL to the image of the avatar sprite sheet. (only PNG images are supported) |
| frame_width | Width of a frame. The original image width must be divided by the frame_width. It must range between a minimum of 1 and a maximum of the image width. The values of frame_width and frame_height can be different. |
| frame_height | Height of a frame. The original image height must be divided by the frame_height. It must range between a minimum of 1 and a maximum of the image height. This must be a multiple of an original image size, ranging between a minimum of 1 and a maximum of 256. The values of frame_width and frame_height can be different. | 
| animations | Animation list of the avatar (idle, moving, jumping, etc…) | 

The animation of the NFT avatar is defined under “animations.” The 17 motions are defined: directional movement, involving jump, attack and idle, and dancing. The following array of movements was included in the metadata. Below is an example of the definition of “animations”

```JSON Schema...
{
"animations": {
	“down”: {
            frames: [1, 2, 3, 4],
            frame_rate: 8,
            repeat: -1
        },
        “left”: {
            frames: [6, 7, 8, 9],
            frame_rate: 8,
            repeat: -1
        },
        “right”: {
            frames: [11, 12, 13, 14],
            frame_rate: 8,
            repeat: -1
        },
        “up”: {
            frames: [16, 17, 18, 19],
            frame_rate: 8,
            repeat: -1
        },
        “dance”: {
            frames: [20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37],
            frame_rate: 8,
            repeat: 1,
        },
        “down_jump”: {
            frames: [38],
            frame_rate: 8,
            repeat: -1
        },
        “left_jump”: {
            frames: [39],
            frame_rate: 8,
            repeat: -1
        },
        “right_jump”: {
            frames: [40],
            frame_rate: 8,
            repeat: -1
        },
        “up_jump”: {
            frames: [41],
            frame_rate: 8,
            repeat: -1
        },
        “down_attack”: {
            frames: [42],
            frame_rate: 8,
            repeat: 1,
        },
        “left_attack”: {
            frames: [43],
            frame_rate: 8,
            repeat: 1,
        },
        “right_attack”: {
            frames: [44],
            frame_rate: 8,
            repeat: 1,
        },
        “up_attack”: {
            frames: [45],
            frame_rate: 8,
            repeat: 1,
        },
        “down_idle”: {
            frames: [0],
            frame_rate: 1,
            repeat: 1,
        },
        “left_idle”: {
            frames: [5],
            frame_rate: 1,
            repeat: 1,
        },
        “right_idle”: {
            frames: [10],
            frame_rate: 1,
            repeat: 1,
        },
        “up_idle”: {
            frames: [15],
            frame_rate: 1,
            repeat: 1,
        },
     }
 }
```

The definition of each motion is as follows. We highly recommend all the animations should be defined. Please note that if the animation is not defined, it can cause undefined behavior (e.g., previous animation can be played).
| Variable | Description |
| ----------- | ----------- |
| down | The downward movement of the avatar. | 
| left | The movement of the avatar to the left. | 
| right | The movement of the avatar to the right. | 
| up | The upward movement of the avatar. | 
| dance | The dance movement of the avatar. | 
| down_jump | The downward jump movement of the avatar. |
| left_jump | The jumping movement of the avatar to the left. |
| right_jump | The jumping movement of the avatar to the right. |
| up_jump | The upward jump movement of the avatar. |
| down_attack | The downward attack movement of the avatar. |
| left_attack | The attack movement of the avatar to the left. |
| right_attack | The attack movement of the avatar to the right. |
| up_attack | The upward attack movement of the avatar. |
| down_idle | The downward idle movement of the avatar. |
| left_idle | The idle movement of the avatar to the left. |
| right_idle | The idle movement of the avatar to the right. |
| up_idle | The upward idle movement of the avatar. | 

Each motion is specified with an array of frames, frame_rate, and repeat. 
| Variable | Description |
| ----------- | ----------- |
| frames | Frame index of the sprite sheet (zero-based). Each frame has (frame_width X frame_height) image fragment in the sprite sheet image. The frame index starts from 0. The maximum array length is 256. | 
| frame_rate | frame_rate must be between a minimum of 1 and a maximum of 64. frame_rate represents the number of frames per second. | 
| repeat | The number of repetitions of the animation. Only two values are supported: -1 and 1. If it is set to -1, it repeats endlessly. If 1, it repeats once. | 

## Backward Compatibility 
This standard can be fully EIP-721, EIP-1155, KIP-17, and KIP-37 compatible by adding an extension “avatars” attribute in the metadata. This allows developers to easily adopt the standard quickly.

## Reference
- [ERC-721](https://eips.ethereum.org/EIPS/eip-721) Non-Fungible Token Standard 
- [ERC-1155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1155.md#erc-1155-metadata-uri-json-schema) Multi-Token Standard 
- [Opensea Metadata Standards](https://docs.opensea.io/docs/metadata-standards)

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).


