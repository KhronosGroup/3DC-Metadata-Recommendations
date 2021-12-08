<!--
Copyright 2021 The Khronos Group Inc.

SPDX-License-Identifier: CC-BY-4.0
-->

![](https://www.khronos.org/assets/images/api_logos/3dcommerce.svg)

# Recommendations for KHR_xmp_json_ld usage in glTF

_Version 0.1.00_\
Last Updated: March 1, 2021

<!-- Start License -->

[![CC4](https://licensebuttons.net/l/by/3.0/88x31.png)](https://creativecommons.org/licenses/by/4.0/)

This work is licensed under a CC BY 4.0 license.

This document is (c) 2021, Khronos Group. Usage and license details are at the end of the document.

<!-- End License -->

## Editors and Alumni

**Editors**\
Alexey Knyazev  
Leonard Daly  
Paul Ko, Microsoft  
Yujin Jung, Samsung  
Jon Wade, Shopify  
Adam Morris, Target

**Alumni**\
Emiliano Gambaretto, Adobe  
Mike Bond, Adobe  
Michael Baele, Adobe  
Andy Glass, Amazon  
Ashleigh Miller, Amazon  
Brent Scannell, Autodesk  
Aurélien Vaysset, Emersya  
Renee Rashid, Facebook  
Chris Joel, Google  
Jonas Gustavsson, Ikea  
Martin Enthed, Ikea  
Anton Berg, Ikea  
Nils Andersson Carlén, Ikea  
Sandra Voelker  
Chi Zhang, Jingdong  
Duncan Knarr, Samsung  
Boaz Ashkenazy, Simply Augmented  
Beau Perschall, TurboSquid  
Eric Chadwick, Wayfair  
Tim Hagberg, Wayfair  
Megan Cassidy, Wayfair

# Table of Contents

- [Recommendations for KHR_xmp_json_ld usage in glTF](#recommendations-for-khr_xmp_json_ld-usage-in-gltf)
  - [Editors and Alumni](#editors-and-alumni)
  - [Content](#content)
- [Overview](#overview)
- [Model 3D namespace](#model-3d-namespace)
- [Recommended XMP Fields for 3D Models](#recommended-xmp-fields-for-3d-models)
  - [Basic Example](#basic-example)
  - [Language Example](#language-example)
  - [Example fields and values for All Rights Reserved implementation](#example-fields-and-values-for-all-rights-reserved-implementation)
  - [CC XMP example](#cc-xmp-example)
- [Sample 3D models](#sample-3d-models)
- [Supporting Tooling and Viewers](#supporting-tooling-and-viewers)
- [Copyright Header](#copyright-header)

# Overview

This document outlines recommended XMP fields for use with 3D models primarily using [glTF](https://github.com/KhronosGroup/glTF/) and the [KHR_xmp_json_ld](https://github.com/KhronosGroup/glTF/tree/master/extensions/2.0/Khronos/KHR_xmp_json_ld) extension. While all [XMP standardized fields](https://github.com/adobe/xmp-docs), such as [Dublin Core](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md), are usable with 3D models, the goal of this document is to align the industry on some important fields to allow tooling and viewers a subset of XMP fields which can be depended on. Additionally, this document specifies the `model3d` XMP namespace which contains fields specific to 3D models.

While this document does primarily focus on glTF and the KHR_xmp extension, the authors' hope is to provide basic guidelines for XMP usage within other 3D formats as well.

# Model 3D namespace

The `model3d` namespace provides properties relevant to 3D models not found in other namespaces.

The namespace URI is https://schema.khronos.org/model3d/xsd/1.0/

| Field Name                | Description                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                            | Type                                                                                                             |
| ------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| model3d:spdxLicense       | Contains the standardized identifier defined in the [SPDX license list](https://spdx.org/licenses/) for this resource. The intent of this field is to provide a machine-readable identification of the content license.                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                | [Text](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#text)          |
| model3d:preferredSurfaces | An array of strings to indicate the preferred surfaces that an object rests on or attach to. The intent is to provide hints for AR viewers about the ideal locations for object placement without being prescriptive or restricting placement on other surface types. Direction terms like “up” and “down” in the following fields refer to the surface normal of the plane or anchor point in the world.Current standardized values are:<br/><ul> <li>`horizontal_up` - Objects resting on top of a horizontal surface (e.g. resting on a table or floor surface that has an upward facing normal)</li><li>`horizontal_down` - Objects that are suspended from a horizontal surface (e.g. hanging from a ceiling that has a normal pointing downwards)</li><li>`vertical` - Objects attached to vertical surfaces (e.g. hanging on a wall or attached to a wall)</li><li>`human_face` - Objects intended to be worn or displayed on a human face</li></ul><br/>This string is left open for custom values, but it is recommeded that the standardized values are used | Array of [Text](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#text) |

# Recommended XMP Fields for 3D Models

In addition to the `model3d` namespace, there are a number of exisiting fields in definied XMP namespaces to help identify and describe the contents of a 3D model. The following list contains suggested fields that users adopt:

| Field Name                                                                                        | Description                                                                                                                                                                                     | Type                                                                                                                                    |
| ------------------------------------------------------------------------------------------------- | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------- |
| [dc:creator](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                   | Creator of the model                                                                                                                                                                            | Array of [ProperName](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#propername)            |
| [dc:description](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)               | Description of the model                                                                                                                                                                        | [Language Alternative](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#language-alternative) |
| [dc:language](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                  | Language of the content in this model. This represents the languages used in the geometry and texture maps of the model                                                                         | Array of [Locale](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#locale)                    |
| [dc:rights](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                    | Human readable license field to compliment the SPDX entry                                                                                                                                       | [Language Alternative](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#language-alternative) |
| [dc:title](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                     | Title of the model                                                                                                                                                                              | [Language Alternative](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#language-alternative) |
| [xmp:CreateDate](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmp.md)              | Original creation date of model                                                                                                                                                                 | [Date](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#date)                                 |
| [xmp:MetadataDate](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmp.md)            | Date of last update to metadata                                                                                                                                                                 | [Date](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#date)                                 |
| [xmp:ModifyDate](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmp.md)              | Date of last update to model contents                                                                                                                                                           | [Date](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#date)                                 |
| [xmpRights:Owner](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md)       | Identifies the IP owner of the 3D asset                                                                                                                                                         | Array of [ProperName](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#propername)            |
| [xmpRights:UsageRights](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md) | Instructions on how a resource can be legally used                                                                                                                                              | [Language Alternative](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#language-alternative) |
| [xmpRights:Marked](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md)      | Indicates if an asset is a rights managed or within the public domain. When true, the asset is managed by copyright, trademark or other marking. When false, the asset is in the public domain. | [Boolean](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/XMPDataTypes/CoreProperties.md#boolean)                           |

## Basic Example

The following is example metadata that could be used for the glTF “[Damaged Sci-fi Helmet](https://github.com/KhronosGroup/glTF-Sample-Models/tree/master/2.0/DamagedHelmet)” sample model.

| Fields Used in Example                                                              |
| ----------------------------------------------------------------------------------- |
| [dc:description](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md) |
| [dc:rights](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)      |
| [dc:title](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)       |
| [dc:relation](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)    |
| [model3d:spdxLicense](#model-3d-namespace)                                          |

```json
{
  "packets": [
    {
      "@context": {
        "dc": "http://purl.org/dc/elements/1.1/",
        "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
        "model3d": "https://schema.khronos.org/model3d/xsd/1.0/"
      },
      "@id": "",
      "dc:description": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "The original model was built on an early draft of glTF 2.0 that did not become final. This new model has been imported and re-exported from Blender to bring it into alignment with the final release glTF 2.0 specification."
        }
      },
      "model3d:spdxLicense": "CC-BY-NC-4.0",
      "dc:relation": {
        "@set": [
          "https://sketchfab.com/theblueturtle_",
          "https://sketchfab.com/models/b81008d513954189a063ff901f7abfe4"
        ]
      },
      "dc:rights": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "By theblueturtle_(https://sketchfab.com/theblueturtle_), published under a Creative Commons Attribution-NonCommercial license."
        }
      },
      "dc:title": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "Battle Damaged Sci-fi Helmet - PBR"
        }
      }
    }
  ]
}
```

## Language Example

This example demonstrates how to include indication of the language of written text on an asset and/or metadata in multiple languages using XMP's Language Alternatives feature. Use the dc:language field to specify what language is used on the asset, not in the metadata. For metadata internationalization, use XMP's Language Alternatives.

| Fields Used in Example                                                              |
| ----------------------------------------------------------------------------------- |
| [dc:description](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md) |
| [dc:language](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)    |
| [dc:title](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)       |
| [model3d:spdxLicense](#model-3d-namespace)                                          |

```json
{
  "packets": [
    {
      "@context": {
        "dc": "http://purl.org/dc/elements/1.1/",
        "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
        "model3d": "https://schema.khronos.org/model3d/xsd/1.0/"
      },
      "@id": "",
      "dc:description": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "This is an example using language alternatives."
        },
        "rdf:_2": {
          "@language": "de-de",
          "@value": "Dies ist ein Beispiel für die Verwendung von Language Alternatives."
        }
      },
      "model3d:spdxLicense": "CC-BY-NC-4.0",
      "dc:title": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "Model with text in a texture"
        }
      }
    }
  ]
}
```

## Example fields and values for All Rights Reserved implementation

This example shows the bare minimum metadata recommended for files that are not in the public domain, and protected by copyright or other marked situations.

xmpRights:UsageTerms should be used in this situation to include legalese indicating what end-users can do with this asset. We recommend that basic copyright terms should be included within the dc:rights field.

| Fields Used in Example                                                                           |
| ------------------------------------------------------------------------------------------------ |
| [dc:creator](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                  |
| [dc:description](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)              |
| [dc:title](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                    |
| [dc:rights](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                   |
| [xmpRights:Marked](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md)     |
| [xmp:MetadataDate](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmp.md)           |
| [xmpRights:UsageTerms](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md) |
| [xmpRights:Owner](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md)      |

```json
{
  "packets": [
    {
      "@context": {
        "dc": "http://purl.org/dc/elements/1.1/",
        "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
        "xmp": "http://ns.adobe.com/xap/1.0/",
        "xmpRights": "http://ns.adobe.com/xap/1.0/rights/"
      },
      "@id": "",
      "dc:creator": {
        "@list": ["Khronos 3DCommerce Working Group"]
      },
      "dc:description": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "Example XMP metadata demonstrating how to include All Rights Reserved metadata."
        }
      },
      "dc:title": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "All Rights Reserved Example"
        }
      },
      "xmp:MetadataDate": "2020-08-01T12:00Z",
      "xmpRights:Marked": true,
      "xmpRights:UsageTerms": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "This work is copyright 2020 by The Khronos Group, Inc. All Rights Reserved. You are not permitted to share or use this in any derivative works."
        }
      },
      "xmpRights:Owner": "The Khronos Group, Inc."
    }
  ]
}
```

## CC XMP example

When using Creative Commons licensing, we recommend that creators additionally use the guidelines for specifying license information provided by Creative Commons.
It is strongly advised to also include the SPDX code for the Creative Commons license you are using in the model3d:license field. This provides a machine-readable format for viewers and tooling.
This example shows the bare minimum metadata recommended for files using Creative Commons licensing.

| Fields Used in Example                                                                           |
| ------------------------------------------------------------------------------------------------ |
| [dc:creator](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                  |
| [dc:description](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)              |
| [dc:title](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/dc.md)                    |
| [xmp:MetadataDate](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmp.md)           |
| [xmpRights:Marked](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md)     |
| [xmpRights:UsageTerms](https://github.com/adobe/xmp-docs/blob/master/XMPNamespaces/xmpRights.md) |
| [model3d:spdxLicense](#model-3d-namespace)                                                       |

```json
{
  "packets": [
    {
      "@context": {
        "dc": "http://purl.org/dc/elements/1.1/",
        "rdf": "http://www.w3.org/1999/02/22-rdf-syntax-ns#",
        "xmp": "http://ns.adobe.com/xap/1.0/",
        "xmpRights": "http://ns.adobe.com/xap/1.0/rights/",
        "model3d": "https://schema.khronos.org/model3d/xsd/1.0/"
      },
      "@id": "",
      "dc:creator": ["Khronos 3DCommerce Working Group"],
      "dc:description": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "Example XMP metadata demonstrating how to include Creative Commons rights metadata."
        }
      },
      "dc:title": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "Creative Commons Example"
        }
      },
      "xmp:MetadataDate": "2020-08-01T12:00Z",
      "xmpRights:Marked": false,
      "xmpRights:UsageTerms": {
        "@type": "rdf:Alt",
        "rdf:_1": {
          "@language": "en-us",
          "@value": "This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License."
        }
      },
      "model3d:spdxLicense": "CC-BY-4.0"
    }
  ]
}
```

# Sample 3D models

Example 3D Models with XMP metadata can be found in the glTF Sample Models repository, such as the Transmission Test model.

# Supporting Tooling and Viewers

Tools and viewers that support both writing and reading KHR_xmp metadata with glTF can be found under the metadata tag in the glTF Project Explorer.

# Copyright

Copyright 2021, The Khronos Group Inc. This Document is protected by copyright laws and contains material proprietary to Khronos. Except as described by these terms, it or any components may not be reproduced, republished, distributed, transmitted, displayed, broadcast or otherwise exploited in any manner without the express prior written permission of Khronos.

Khronos grants a conditional copyright license to use and reproduce the unmodified Document for any purpose, without fee or royalty, EXCEPT no licenses to any patent, trademark or other intellectual property rights are granted under these terms.

Khronos makes no, and expressly disclaims any, representations or warranties, express or implied, regarding this Document, including, without limitation: merchantability, fitness for a particular purpose, non-infringement of any intellectual property, correctness, accuracy, completeness, timeliness, and reliability. Under no circumstances will Khronos, or any of its Promoters, Contributors or Members, or their respective partners, officers, directors, employees, agents or representatives be liable for any damages, whether direct, indirect, special or consequential damages for lost revenues, lost profits, or otherwise, arising from or in connection with these materials.

Khronos® and Vulkan® are registered trademarks, and ANARI™, WebGL™, glTF™, NNEF™, OpenVX™, SPIR™, SPIR-V™, SYCL™, OpenVG™ and 3D Commerce™ are trademarks of The Khronos Group Inc. OpenXR™ is a trademark owned by The Khronos Group Inc. and is registered as a trademark in China, the European Union, Japan and the United Kingdom. OpenCL™ is a trademark of Apple Inc. and OpenGL® is a registered trademark and the OpenGL ES™ and OpenGL SC™ logos are trademarks of Hewlett Packard Enterprise used under license by Khronos. ASTC is a trademark of ARM Holdings PLC. All other product names, trademarks, and/or company names are used solely for identification and belong to their respective owners.
