---
kip: 87
title: NFT Avatar in Multi-Metaverse
author: Yeri Lee (@yeri-lee), Junghyun Colin Kim (@kjhman21), Wonbae Kim (@kernys), Seokrin Sung (@taronsung)
discussions-to: https://forum.klaytn.foundation/t/en-kip-87-nft-avatar-standard-proposal/6161
status: Draft
type: Standards Track
category: Application
created: 2022-11-01
requires: 17, 37
---

## Simple Summary
Creating an NFT avatar standard to provide an interchangeable visualization of NFT across multiple metaverses.

## Abstract
Although fungible tokens (FTs) are easily exchangeable across different platforms through DEX, non-fungible tokens (NFTs) do not easily migrate from one metaverse to another. The exchange of NFTs across platforms often does not promise the equivalent asset value, including quality and style. We aim to define an NFT as a single character with different visualization for multi-metaverse. An NFT character with the standard definition and predefined motion images can create an adequate visualization when entering metaverses as an NFT avatar. The NFT avatar standard will increase the utility of NFT, invigorate the metaverse industry and strengthen interoperability.

## Motivation
NFT has different utilities. Some are used as an asset in the gaming industry while some are used as a parcel of virtual land in the metaverse. The usage of NFTs has often been limited to PFP (profile picture) until today. Yet, an NFT character should be interchanged into several forms of avatars corresponding to the metaverse platform it enters. This standard distinguishes the usage between NFT characters as absolute graphical assets and NFT avatars as motion-added chameleon-ed NFT characters.

With the NFT avatar standard, NFT characters will transfer into avatars enabling use cases within multiple metaverses. The character purchased in the NFT marketplace can enter as a 2D avatar in Zep.us while it enters Another.world as a 3D avatar. In addition, user-created 3D avatars, like VR Chat, can also compatibly enter multi-metaverse as NFT avatars.

The NFT avatar standard will generate a positive value creation cycle between creators, the NFT marketplace, and the metaverse. Each individual entity will have a common standard to share, maximizing the utility and interoperability of NFTs. With the standard, the value of an item minted by creators will be increased with heightened practicality and utilization. This will boost the activity within NFT marketplaces while the usage of NFT within metaverses also increases. The versatile utility of NFT characters will increase the public desire to purchase and incentivize creators to generate, ultimately vitalizing the creator economy. Likewise, such dynamics will unleash NFT characters in the multi-metaverse.

## Specification
The keywords “MUST”, “MUST NOT”, “REQUIRED”, “SHALL”, “SHALL NOT”, “SHOULD”, “SHOULD NOT”, “RECOMMENDED”, “MAY” and “OPTIONAL” in this document are to be interpreted as described in RFC 2119.

As an a metadata extension of [ERC-721](https://eips.ethereum.org/EIPS/eip-721) and [EIP-4955](https://eips.ethereum.org/EIPS/eip-4955), the NFT avatar standard supplements the "zep" section under "namespaces". The data required for the avatar varies by metaverse platform. In the instance of Zep, type of asset and properties of image are defined to maximize the scalability of individual NFT.

## Schema
In addition to [EIP-4955](https://eips.ethereum.org/EIPS/eip-4955), we define more in-depth specification to represent an avatar in various metaverses.

Here is the schema for this. This schema only defines an avatar schema for [Zep](https://zep.us), but it can be used for various metaverses using similar avatar representation.
```json
{
  "title": "Asset Metadata",
  "type": "object",
  "properties": {
    "name": {
      "type": "string",
      "description": "Identifies the asset to which this NFT represents"
    },
    "description": {
      "type": "string",
      "description": "Describes the asset to which this NFT represents"
    },
    "image": {
      "type": "string",
      "description": "A URI pointing to a resource with mime type image/* representing the asset to which this NFT represents. Consider making any images at a width between 320 and 1080 pixels and aspect ratio between 1.91:1 and 4:5 inclusive."
    },
    "namespaces": {
      "type": "object",
      "description": "Projects that needs specific properties to use the NFT",
      "properties": {
        "zep": {
          "$ref": "#/$defs/zep"
        }
      },
      "additionalProperties": {
        "type": "object"
      }
    }
  },
  "$defs": {
    "zep": {
      "title": "Avatar Schema for Zep",
      "type": "object",
      "properties": {
        "type": {
          "type": "string",
          "enum": [ "avatar" ],
          "description": "Type of asset that an item will perform within the metaverse. Currently, only 'avatar' is supported."
        },
        "properties": {
          "type": "object",
          "properties": {
            "image": {
              "type": "string",
              "format": "uri",
              "description": "A URL to the image of the avatar sprite sheet. (only PNG images are supported)"
            },
            "frame_width": {
              "type": "integer",
              "minimum": 1,
              "description": "Width of a frame. The original image width must be divided by the frame_width. It must range between a minimum of 1 and a maximum of the image width. The values of frame_width and frame_height can be different."
            },
            "frame_height": {
              "type": "integer",
              "minimum": 1,
              "maximum": 256,
              "description": "Height of a frame. The original image height must be divided by the frame_height. It must range between a minimum of 1 and a maximum of the image height. This must be a multiple of an original image size, ranging between a minimum of 1 and a maximum of 256. The values of frame_width and frame_height can be different."
            },
            "animations": {
              "type": "object",
              "properties": {
                "down": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The downward movement of the avatar."
                },
                "left": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The movement of the avatar to the left."
                },
                "right": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The movement of the avatar to the right."
                },
                "up": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The upward movement of the avatar."
                },
                "dance": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The dance movement of the avatar."
                },
                "down_jump": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The downward jump movement of the avatar."
                },
                "left_jump": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The jumping movement of the avatar to the left."
                },
                "right_jump": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The jumping movement of the avatar to the right."
                },
                "up_jump": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The upward jump movement of the avatar."
                },
                "down_attack": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The downward attack movement of the avatar."
                },
                "left_attack": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The attacking movement of the avatar to the left."
                },
                "right_attack": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The attacking movement of the avatar to the right."
                },
                "up_attack": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The upward attack movement of the avatar."
                },
                "down_idle": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The downward idle movement of the avatar."
                },
                "left_idle": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The idleing movement of the avatar to the left."
                },
                "right_idle": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The idleing movement of the avatar to the right."
                },
                "up_idle": {
                  "$ref": "#/$defs/zep/$defs/animationDef",
                  "description": "The upward idle movement of the avatar."
                }
              },
              "required": [
                "down",
                "left",
                "right",
                "up",
                "dance",
                "down_jump",
                "left_jump",
                "right_jump",
                "up_jump",
                "down_attack",
                "left_attack",
                "right_attack",
                "up_attack",
                "down_idle",
                "left_idle",
                "right_idle",
                "up_idle"
              ]
            }
          },
          "required": [
            "image",
            "frame_width",
            "frame_height",
            "animations"
          ]
        }
      },
      "required": [ "type", "properties" ],
      "$defs": {
        "animationDef": {
          "type": "object",
          "properties": {
            "frames": {
              "type": "array",
              "items": "integer",
              "maxItems": 256,
              "description": "Frame index of the sprite sheet (zero-based). Each frame has (frame_width X frame_height) image fragment in the sprite sheet image. The frame index starts from 0. The maximum array length is 256."
            },
            "frame_rate": {
              "type": "integer",
              "minimum": 1,
              "maximum": 64,
              "description": "frame_rate must be between a minimum of 1 and a maximum of 64. frame_rate represents the number of frames per second."
            },
            "repeat": {
              "type": "integer",
              "enum": [-1, 1],
              "description": "The number of repetitions of the animation. Only two values are supported: -1 and 1. If it is set to -1, it repeats endlessly. If 1, it repeats once."
            }
          },
          "required": [ "frames", "frame_rate", "repeat" ]
        }
      }
    }
  }
}
```

### Example

Here is an example of the schema.

```json
{
  "name": "Klaytn Core",
  "description": "Klaytn Story NFTs - Core",
  "image": "https://klaytn-story-bucket.s3.ap-northeast-2.amazonaws.com/core-face.png",
  "namespaces": {
    "zep": {
      "type": "avatar",
      "properties": {
        "image": "https://klaytn-story-bucket.s3.ap-northeast-2.amazonaws.com/core-sheet.png",
        "frame_width": 48,
        "frame_height": 64,
        "animations": {
          "down": {
            "frames": [ 1, 2, 3, 4 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "left": {
            "frames": [ 6, 7, 8, 9 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "right": {
            "frames": [ 11, 12, 13, 14 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "up": {
            "frames": [ 16, 17, 18, 19 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "dance": {
            "frames": [ 20, 21, 22, 23, 24, 25, 26, 27, 28, 29, 30, 31, 32, 33, 34, 35, 36, 37 ],
            "frame_rate": 8,
            "repeat": 1
          },
          "down_jump": {
            "frames": [ 38 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "left_jump": {
            "frames": [ 39 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "right_jump": {
            "frames": [ 40 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "up_jump": {
            "frames": [ 41 ],
            "frame_rate": 8,
            "repeat": -1
          },
          "down_attack": {
            "frames": [ 42 ],
            "frame_rate": 8,
            "repeat": 1
          },
          "left_attack": {
            "frames": [ 43 ],
            "frame_rate": 8,
            "repeat": 1
          },
          "right_attack": {
            "frames": [ 44 ],
            "frame_rate": 8,
            "repeat": 1
          },
          "up_attack": {
            "frames": [ 45 ],
            "frame_rate": 8,
            "repeat": 1
          },
          "down_idle": {
            "frames": [ 0 ],
            "frame_rate": 1,
            "repeat": 1
          },
          "left_idle": {
            "frames": [ 5 ],
            "frame_rate": 1,
            "repeat": 1
          },
          "right_idle": {
            "frames": [ 10 ],
            "frame_rate": 1,
            "repeat": 1
          },
          "up_idle": {
            "frames": [ 15 ],
            "frame_rate": 1,
            "repeat": 1
          }
        }
      }
    }
  }
}
```

## Backward Compatibility 
This standard can be fully [ERC-721](https://eips.ethereum.org/EIPS/eip-721), [ERC-1155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1155.md#erc-1155-metadata-uri-json-schema), [EIP-4955](https://eips.ethereum.org/EIPS/eip-4955), [KIP-17](https://kips.klaytn.foundation/KIPs/kip-17), and [KIP-37](https://kips.klaytn.foundation/KIPs/kip-37) compatible by adding an extension “avatars” attribute in the metadata. This allows developers to easily adopt the standard quickly.

## Reference
- [ERC-721](https://eips.ethereum.org/EIPS/eip-721) Non-Fungible Token Standard
- [ERC-1155](https://github.com/ethereum/EIPs/blob/master/EIPS/eip-1155.md#erc-1155-metadata-uri-json-schema) Multi-Token Standard 
- [EIP-4955](https://eips.ethereum.org/EIPS/eip-4955)
- [KIP-17](https://kips.klaytn.foundation/KIPs/kip-17)
- [KIP-37](https://kips.klaytn.foundation/KIPs/kip-37)
- [Decentraland Docs](https://docs.decentraland.org/creator/wearables/linked-wearables/)

## Copyright
Copyright and related rights waived via [CC0](https://creativecommons.org/publicdomain/zero/1.0/).
