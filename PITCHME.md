---?image=assets/images/gitpitch-audience.jpg
@title[Platform Config DB (PCD)]
<br><br><br><br><br>
## <span class="gold"   >UEFI & EDK II Training</span>

#### Platform Configuration Database (PCD)

<br>
<span style="font-size:0.75em" ><a href='http://www.tianocore.org'>tianocore.org</a></span>
Note:
  PITCHME.md for UEFI / EDK II Training  Platform Config DB (PCD) Pres

  Copyright (c) 2018, Intel Corporation. All rights reserved.<BR>

  Redistribution and use in source (original document form) and 'compiled'
  forms (converted to PDF, epub, HTML and other formats) with or without
  modification, are permitted provided that the following conditions are met:

  1) Redistributions of source code (original document form) must retain the
     above copyright notice, this list of conditions and the following
     disclaimer as the first lines of this file unmodified.

  2) Redistributions in compiled form (transformed to other DTDs, converted to
     PDF, epub, HTML and other formats) must reproduce the above copyright
     notice, this list of conditions and the following disclaimer in the
     documentation and/or other materials provided with the distribution.

  THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR
  IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF
  MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO
  EVENT SHALL TIANOCORE PROJECT  BE LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL,
  SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO,
  PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS;
  OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY,
  WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR
  OTHERWISE) ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF
  ADVISED OF THE POSSIBILITY OF SUCH DAMAGE.



---  
@title[Lesson Objective]
<BR>
### <p align="center"<span class="gold"   >Lesson Objective </span></p><br>

<!---  Add bullets using https://fontawesome.com/cheatsheet certificate
-->
<br>
<ul style="list-style-type:none">
 <li>@fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Define Platform Configuration Database (PCD) and &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;explain the syntax</span> </li>
 <li>@fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Differentiate types of PCDs</span></li>
 <li>@fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Explain how changing a PCD value affects output</span> </li>
 <li>@fa[certificate gp-bullet-magenta]<span style="font-size:0.9em">&nbsp;&nbsp;Evaluate the results of a PCD value modification</span></li>
</ul>

---?image=assets/images/binary-strings-black2.jpg
@title[PCD Overview Section]
<br><br><br><br><br><br><br>
### <span class="gold"  >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PCD Overview</span>
<span style="font-size:0.9em" >&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;</span>

---
@title[EDK II PCD’s Purpose and Goals]
<br>
<p align="right"><span class="gold" >EDK II PCD’s Purpose and Goals</span></p>
@fa[github gp-bullet-gold]<span style="font-size:0.7em">&nbsp;&nbsp;Documentaton :  <a href="https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Universal/PCD/Dxe/Pcd.inf"> MdeModulePkg/Universal/PCD/Dxe/Pcd.inf  </a> </span>
<br>
<div class="left1">
<span style="font-size:01.0em" ><font color="cyan">Purpose</font></span>
<ul>
  <li><span style="font-size:0.8em" >Establishes platform common definitions </span>  </li>
  <li><span style="font-size:0.8em" >Build-time/Run-time aspects </span>  </li>
  <li><span style="font-size:0.8em" >Binary Editing Capabilities </span>  </li>
</ul>
</div>
<div class="right1">
<span style="font-size:01.0em" ><font color="cyan">Goals</font></span>
<ul>
  <li><span style="font-size:0.8em" >Simplify porting </span>  </li>
  <li><span style="font-size:0.8em" >Easy to associate with a module or platform </span>  </li>
</ul>
</div>

Note:

### Common definitions are established for platform component settings
- Standardize exposure of platform & module settings
- Help with Platform Porting
### Build-time aspects
- Component information is collected from PCD definitions that are associated with a given module
### Run-time aspects
- APIs are provided which allow access to component settings during the operation of the platform
### Binary Editing Capabilities
- A module can carry its own PCD data in the binary image and have it exposed so the data can be edited in the flash image

+++
@title[EDK II PCD’s Purpose and Goals]
<br>
<p align="right"><span class="gold" >EDK II PCD’s Purpose and Goals</span></p>
@fa[github gp-bullet-gold]<span style="font-size:0.7em">&nbsp;&nbsp;Documentaton :  <a href="https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Universal/PCD/Dxe/Pcd.inf"> MdeModulePkg/Universal/PCD/Dxe/Pcd.inf  </a> </span>
<br>
```c
/**
 ////////////////////////////////////////////////////////////////////////////////
 //                      Introduction of PCD database                          //
 ////////////////////////////////////////////////////////////////////////////////

 1, Introduction
    PCD database hold all dynamic type PCD information. The structure of PEI PCD 
    database is generated by build tools according to dynamic PCD usage for 
    specified platform.
    
 2, Dynamic Type PCD
    Dynamic type PCD is used for the configuration/setting which value is determined
    dynamic. In contrast, the value of static type PCD (FeatureFlag, FixedPcd, 
    PatchablePcd) is fixed in final generated FD image in build time. 
 // . . .       
```
@[2-13]( See Link above to view the entire documentation)

Note:

---
@title[PCD Types]
### <p align="right"><span class="gold" >PCD Types</span></p>
@snap[east span-35]
@box[bg-lt-blue-pp text-white rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > FeatureFlag</span></p>)
<br>
@snapend

@snap[north-west span-35]
<br>
<br>
@box[bg-yellow text-blue rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > FixedAtBuild</span></p>)
@snapend


@snap[north span-30]
<br>
<br>
<br>
<br>
@box[bg-green-pp text-white rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > Dynamic</span></p>)
@snapend


@snap[north-east span-30]
<br>
<br>
@box[bg-green-pp text-white rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > DynamicEx</span></p>)
@snapend



@snap[south-west span-30]
@box[bg-green-pp text-white rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > DynamicHii</span></p>)
<br>
<br>
<br>
<br>
<br>
@snapend

@snap[south-east span-30]
@box[bg-green-pp text-white rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > DynamicVpd</span></p>)
<br>
<br>
<br>
<br>
<br>
@snapend


@snap[west span-45]
@box[bg-purple-pp text-white rounded my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-family: Courier New; font-weight: bold;" > PatchableInModule</span></p>)
<br>
@snapend


@snap[south-west span-100]
@box[bg-navy text-white rounded  my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-weight: bold;" > Syntax Examples<br></span><span style="font-size:0.50em;" >`[pcdsFeatureFlag.common] [pcdsFixedAtBuild.IA32]`&nbsp;<br>&nbsp;<br>&nbsp;</span></p>)
@snapend



@snap[south-west span-100]
@box[bg-navy text-white rounded  my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-weight: bold;" > Syntax Examples<br></span><span style="font-size:0.50em;" >`[pcdsFeatureFlag.common] [pcdsFixedAtBuild` <span style="background-color: gray";>`.IA32]`&nbsp;</span><br>&nbsp;<br>&nbsp;</span></p>)
@snapend


@snap[south-west span-100]
@box[bg-navy text-white rounded  my-box-pad fragment ](<p style="line-height:80%" ><span style="font-size:0.80em; font-weight: bold;" > Syntax Examples<br></span><span style="font-size:0.50em;" >`[pcdsFeatureFlag.common] [pcdsFixedAtBuild.IA32]`&nbsp;<br>`[PcdsFixedAtBuild, PcdsPatchableInModule, PcdsDynamic, PcdsDynamicEx]`<br>&nbsp;</span></p>)
@snapend



Note:

#### FeatureFlag 
- Replaces a switch MACRO to enable/disable a feature (TRUE or FALSE)
#### FixedAtBuild
- Replaces a macro that produced a customizable value
- Value of this PCD type is determined at build time and is stored in the code section of a module’s PE image 
#### PatchableInModule
- Value is stored in the data section, rather than the code section, of the module’s PE image. 
#### Dynamic / DyanmicEx / DynamicHii / DynamicVpd
- Value is assigned by one module and is accessed by other modules in execution time 
#### Syntax Examples
- 	[pcdsFeatureFlag.common] [pcdsFixedAtBuild.IA32] [pcdsFixedAtBuild.X64]   [pcdsFixedAtBuild.IPF] [pcdsFixedAtBuild.EBC]   [pcdsDynamic.IA32] [pcdsDynamicEx.X64] 


---?image=/assets/images/slides/SlideUEFI.JPG
@title[UEFI Platform Initialization (PI) 1.x Spec & PCDs]
<br>
<p align="center"><span class="gold" ><b>UEFI Platform Initialization (PI) 1.x Spec & PCDs</b></span></p>
<span style="font-size:01.0em"><font color="yellow"><b>PEI</b></font></span>
<ul>
 <li><span style="font-size:0.8em">PCD PEIM produces PCD database</span> </li>
 <li><span style="font-size:0.8em">Two PCD PPIs: `PCD_PPI`  and  `EFI_PEI_PCD_PPI`</span></li>
</ul>
<br>
<span style="font-size:01.0em"><font color="yellow"><b>DXE</b></font></span>
<ul>
 <li><span style="font-size:0.8em">DXE Driver Manages PCDs</span></li>
 <li><span style="font-size:0.8em">Two PCD Protocols:   `PCD_PROTOCOL`   and `EFI_PCD_PROTOCOL`</span></li>
</ul>

Note:

#### PEI
PCD PEIM produces PCD database to manage all dynamic PCD in PEI and install PCD PPI service

- There are two PCD PPIs:

- PCD_PPI – EDK II implementation to support Dynamic & DynamicEx PCD types
- EFI_PEI_PCD_PPI - Defined by PI Specification 1.x (Vol 3) and only supports DynamicEx PCD type
The DynamicEx PCD type is compatible between the PCD_PPI and EFI_PEI_PCD_PPI


#### DXE
The PCD DXE driver management database contains all dynamic PCD entries initialized in  the PEI/DXE phases and produces an implementation of PCD protocol

- There are two PCD Protocols:

- PCD_PROTOCOL – EDK II implementation to support Dynamic & DynamicEx PCD types
- EFI_PCD_PROTOCOL - Defined by PI Specification 1.x (Vol 3) and only supports DynamicEx PCD type
The PCD DXE driver will produce both protocols at the same time


---?image=/assets/images/slides/Slide14.JPG
@title[PCD Library]
<br>
### <p align="right"><span class="gold" >PCD Library</span></p>
<br>
<div class="left1">
<ul>
 <li><span style="font-size:0.9em"><font color="yellow">Provides interface for PCDs</font></span> </li>
 <li><span style="font-size:0.9em"><font color="white">PCD PPI - PEI</font></span></li>
 <li><span style="font-size:0.9em"><font color="yellow">PCD Protocol – DXE</font></span></li>
 <li><span style="font-size:0.9em"><font color="white">Allows access to data</font></span></li>
</ul>
</div>
<div class="right1">
<span style="font-size:01.0em"><font color="yellow"></font></span>
</div>

Note:

#### Provides PCD usage macro interface for all PCD types.
- Macro should be included in any module using PCD
#### PCD Protocol and PCD PPI
- These are the base PCD service APIs that provide an abstraction for accessing configuration content in the platform
- Allows access to data through size-granular APIs and provides a mechanism for a firmware component to monitor specific settings and be alerted when a setting is changed

---
@title[PCD Library Calls]
<br>
### <p align="right"><span class="gold" >PCD Library Calls</span></p>
<br>
<span style="font-size:0.9em">PCD Protocol and PCD PPI Functions</span>
<div class="left1">
<pre>
```
PcdGetXX()
PcdSetXX()
PcdGetExXX()
PcdSetExXX()
PcdToken()
PCDSetSku()
PcdGetNextToken()
PcdGetNextTokenSpace()
CallBackOnSet()
CancelCallBack()
```
</pre>
</div>
<div class="right1">
<span style="font-size:0.7em"><font color="#87E2A9">Where: "XX" = </font></span>
<pre>
```
8
16
32
Size
Ptr
Boolean
```
</pre>
</div>

Note:
- The PcdGetXX(), PcdSetXX(), PcdToken(), and PcdGetNextTokenSpace() operations are only available prior to ExitBootServices().
- If access to PCD values are required at runtime, then their values must be collected prior to ExitBootServices().


---
@title[PCD Syntax]
### <p align="right"><span class="gold" >PCD Syntax</span></p>
<span style="font-size:0.9em"><font color="white">PCDs can be located anywhere within the Workspace even though a different package will use those PCDs for a given project</font></span>

@snap[west span-30 fragment]
<br>
<br>
<br>
<p align="center"><span style="font-size:01.49em; font-weight: bold;">@color[yellow](.DEC)</span></p>
@box[bg-gold2 text-black waved  ](<span style="font-size:01.280em; font-weight: bold;" >Define <br>PCD</span>)
<br>
@snapend

@snap[midpoint span-30 fragment]
<br>
<br>
<br>
<p align="center"><span style="font-size:01.49em; font-weight: bold;">@color[yellow](.INF)</span></p>
@box[bg-green-pp text-black waved   ](<span style="font-size:01.280em; font-weight: bold;" >Reference PCD</span>)
<br>
@snapend


@snap[east span-30 fragment]
<br>
<br>
<br>
<p align="center"><span style="font-size:01.49em; font-weight: bold;">@color[yellow](.DSC)</span></p>
@box[bg-lt-blue-pp text-black waved  ](<span style="font-size:01.280em; font-weight: bold;" >Modify <br>PCD</span>)
<br>
@snapend

Note:

- The Platform configuration database is generated by the build process parsing the build description files that define and specify PCD entries.

- What we see on this slide is how the PCD data is being used in various levels of the build description files

- First we have the DEC file – this Defines a list of PCD tokens that modules can use. 
 	It Defines the PCD entries that will exist under the GUID for that  package, the PCD restriction, valid types for the PCD, and a default value for the PCD. There is a whole syntax and how to define a PCD in the DEC file.

- Next we have PCB entries in the INF file- and this Defines the usage of PCD tokens by the module.
	It Defines what PCD entries are being used within the module, the PCD restriction (or DYNAMIC for none), and a Optional default value for the PCD within this module only.

- Next is the DSC file – This is at the Platform level and describes the contents of the build for a specific platform. 
	PCD entries are assigned values and types for the platform build. You would define a value here to be used by that platform. The value could be different when it is defined in the DEC file but the value in the DSC would be the final value . And They Cannot conflict with established restrictions.

- Not on this slide but also there is the FDF build description File – and this file would have flash layout related values 


#### additional notes 
##### DEC:
- Defines list of PCD tokens that modules can use.

- Defines the PCD entries that will exist under the GUID for that  package, the PDC restriction, valid types for the PCD, and a default value for the PCD.
- The DEC file is part of a package.  Any package may define PCD entries. Any module that depends on a package may use the PCD entries defined in that packages' DEC file  

##### INF:
- Defines usage of PCD tokens by the module

- Defines what PCD entries are being used within the module, the PCD restriction (or DYNAMIC for none), and a default value for the PCD within this module only.
- The INF file also carries descriptive text for a given PCD entry


##### DSC:
- Platform level file which describes the contents of the build for a specific platform.
- PCD entries are assigned values and types for the platform build.  Cannot conflict with established restrictions.
- In most cases, PCD entries do not have SKU enabled and have a single value associated with them. However, a SKU PCD entry may have multiple values.


---?image=/assets/images/slides/Slide21.JPG
@title[PCD Syntax example]
### <p align="right"><span class="gold" >PCD Syntax Example</span></p>

@snap[north-east span-90 fragment]
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:0.9em; ">PCD defined in the DEC file from any package</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[Guids.common]<br>&nbsp;&nbsp;@color[red](PcdTokenSpaceGuidName)={ 0xXXXXXXXX, 0xXXXX, 0xXXXX, { 0xXX, . . .}}<br>&nbsp;&nbsp;. . .<br>&nbsp;&nbsp;[Pcds...]<br>&nbsp;&nbsp;PcdTokenSpaceGuidName.PcdTokenName|Value[|DatumType[|MaxSize]]|Token<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend

@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:0.9em; ">PCD usage listed in INF file for module</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[...Pcds...]<br>&nbsp;&nbsp;PcdTokenSpaceGuidName.@color[red](PcdTokenName)|[Value]<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:0.9em; ">Value of PCD set in Platform DSC</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[Pcds...]<br>&nbsp;&nbsp;PcdTokenSpaceGuidName.@color[red](PcdTokenName)|Value[|DatumType[|MaximumDatumSize]]</span><br>&nbsp;&nbsp;</p>)
<br>
@snapend

Note:




---?image=/assets/images/slides/Slide26.JPG
@title[PCD Variable example]
### <p align="right"><span class="gold" >PCD Variable Example</span></p>


@snap[north-east span-90 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.9em; ">
<br>
<br>
@color[yellow](Defined)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild, PcdsPatchableInModule]<br>&nbsp;&nbsp;gEfiMdeModulePkgTokenSpaceGuid.@color[red](PcdMaxVariableSize)|0x400|UINT32|0x30000003<br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-90 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; ">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>@color[yellow](Referenced)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[Pcd]<br>&nbsp;&nbsp;gEfiMdeModulePkgTokenSpaceGuid.@color[red](PcdMaxVariableSize)  &num;&num; CONSUMES<br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>@color[yellow](Modified)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild]<br>&nbsp;&nbsp;gEfiMdeModulePkgTokenSpaceGuid.@color[red](PcdMaxVariableSize)|<font color="cyan">0x008400</font><br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
@color[yellow](Used)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;MdeModulePkg\Universal\Variable\RuntimeDxe\Variable.c  // max NV variable size <br>&nbsp;&nbsp;mVariableModuleGlobal->MaxVariableSize = PcdGet32 (@color[red](PcdMaxVariableSize));<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend



@snap[north-east span-90 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>@color[yellow](Modified)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsFixedAtBuild]<br>&nbsp;&nbsp;gEfiMdeModulePkgTokenSpaceGuid.@color[red](PcdMaxVariableSize)|<span style="background-color: yellow";>@color[green](0x008400)&nbsp;&nbsp;</span><br>&nbsp;&nbsp;</span></p>)
@snapend


Note:

The value that will get used with the source code will be the value modified in the .dsc file.  This is the preferred way of modifying PCD values from their default values



---?image=/assets/images/slides/Slide33.JPG
<!-- .slide: data-transition="none" -->
@title[PCD Software]
### <p align="right"><span class="gold" >PCD Software</span></p>

Note:
- May resolve to API call to call PCD service (DYNAMIC type of calls)

- May resolve to #define equivalent retrieved from Autogen files.
- (FIXED_AT_BUILD type of calls)



+++?image=/assets/images/slides/Slide34.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Software 02]
### <p align="right"><span class="gold" >PCD Software</span></p>

Note:


- May resolve to API call to call PCD service (DYNAMIC type of calls)

- May resolve to #define equivalent retrieved from Autogen files.
- (FIXED_AT_BUILD type of calls)


+++?image=/assets/images/slides/Slide35.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Software 03]
### <p align="right"><span class="gold" >PCD Software</span></p>

Note:


- May resolve to API call to call PCD service (DYNAMIC type of calls)

- May resolve to #define equivalent retrieved from Autogen files.
- (FIXED_AT_BUILD type of calls)


+++?image=/assets/images/slides/Slide36.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Software 04]
### <p align="right"><span class="gold" >PCD Software</span></p>

Note:


- May resolve to API call to call PCD service (DYNAMIC type of calls)

- May resolve to #define equivalent retrieved from Autogen files.
- (FIXED_AT_BUILD type of calls)


+++?image=/assets/images/slides/Slide37.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Software 05]
### <p align="right"><span class="gold" >PCD Software</span></p>



Note:

- May resolve to API call to call PCD service (DYNAMIC type of calls)

- May resolve to #define equivalent retrieved from Autogen files.
- (FIXED_AT_BUILD type of calls)


---?image=/assets/images/slides/Slide39.JPG
<!-- .slide: data-transition="none" -->
@title[PCD Driver]
### <p align="right"><span class="gold" >PCD Driver</span></p>

Note:



+++?image=/assets/images/slides/Slide40.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Driver 02]
### <p align="right"><span class="gold" >PCD Driver</span></p>

Note:



+++?image=/assets/images/slides/Slide41.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Driver 03]
### <p align="right"><span class="gold" >PCD Driver</span></p>

Note:


+++?image=/assets/images/slides/Slide42.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Driver 04]
### <p align="right"><span class="gold" >PCD Driver</span></p>

Note:


+++?image=/assets/images/slides/Slide43.JPG
<!-- .slide: data-background-transition="none" -->
<!-- .slide: data-transition="none" -->
@title[PCD Driver 05]
### <p align="right"><span class="gold" >PCD Driver</span></p>

Note:

---
@title[Fixed PCD AutoGen files]
<p align="right"><span class="gold" ><b>Fixed PCD AutoGen files</b></span></p>
<span style="font-size:0.8em">Example: </span>@fa[github gp-bullet-gold]<span style="font-size:0.5em">&nbsp;&nbsp;<a href="https://github.com/tianocore/edk2/blob/master/MdeModulePkg/Universal/Variable/RuntimeDxe/VariableSmmRuntimeDxe.inf "> MdeModulePkg\Universal\Variable\RuntimeDxe\VariableRuntimeDxe</a> </span>

@snap[north-west span-100 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:01.25em; ">@color[#87E2A9](<b>Autogen.h</b>)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;&num;define _PCD_TOKEN_PcdMaxVariableSize  250U<br>&nbsp;&nbsp;&num;define _PCD_SIZE_PcdMaxVariableSize 4<br>&nbsp;&nbsp;&num;define _PCD_GET_MODE_SIZE_PcdMaxVariableSize  _PCD_SIZE_PcdMaxVariableSize <br>&nbsp;&nbsp;&num;define _PCD_VALUE_PcdMaxVariableSize<span style="background-color: yellow";>@color[green](&nbsp;&nbsp;  0x8400U)&nbsp;&nbsp;</span><br>&nbsp;&nbsp;extern const  UINT32  _gPcd_FixedAtBuild_PcdMaxVariableSize;<br>&nbsp;&nbsp;&num;define _PCD_GET_MODE_32_PcdMaxVariableSize  _gPcd_FixedAtBuild_PcdMaxVariableSize<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend

@snap[north-west span-100 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:80%"><span style="font-size:01.25em; ">@color[#00b0f0](<b>Autogen.c</b>)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;// Definition of PCDs used in this module<br>&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](• • •) <br>&nbsp;&nbsp;GLOBAL_REMOVE_IF_UNREFERENCED const UINT32  \<br>&nbsp;&nbsp;&nbsp;&nbsp;_gPcd_FixedAtBuild_PcdMaxVariableSize = &lowbar;PCD&lowbar;VALUE&lowbar;<span style="background-color: white";>@color[red](PcdMaxVariableSize;)&nbsp;&nbsp;</span><br>&nbsp;&nbsp;</span></p>)

@snapend


Note:


---
@title[What about a Dynamic PCD]
<br>
<p align="left"><span style="font-size:01.2em"><font color="#e49436"><b>What about a Dynamic PCDs?</b></font></span></p>
<br>
<ul style="list-style-type:disc">
 <li><span style="font-size:0.9em">Only can be <b>Set</b> and changed during Boot time. </span> </li>
 <li><span style="font-size:0.9em">PCD can be set with the library Set:  `LibPcdSet… ` </span></li>
 <li><span style="font-size:0.9em">PCD can be retrieved with the library Get: `LibPcdGet…` </span></li>
</ul>
<br>
<br>
<p style="line-height:80%"><span style="font-size:0.8em">Example: &nbsp; Use the variable  <font color="yellow">`PcdPlatformBootTimeOut`</font> defined for the platform time in seconds before booting, modified for a value of <font color="cyan">`03` </font> seconds</span></p>


Note:

Slide says it all

---?image=/assets/images/slides/Slide26_1.JPG
@title[Dynamic PCD]
### <p align="right"><span class="gold" >Dynamic PCD</span></p>


@snap[north-east span-90 fragment]
<p align="left" style="line-height:40%"><span style="font-size:0.9em; ">
<br>
<br>
@color[yellow](Defined)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;[PcdsDynamic]<br>&nbsp;&nbsp;gEfiIntelFrameworkModulePkgTokenSpaceGuid.@color[red](PcdPlatformBootTimeOut)|0xffff|UINT16|0x<br>&nbsp;&nbsp;</span></p>)
@snapend

@snap[north-east span-90 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; ">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>@color[yellow](Modified)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;[PcdsDynamicDefault]<br>&nbsp;gEfiIntelFrameworkModulePkgTokenSpaceGuid.PcdPlatformBootTimeOut|<font color="cyan">`03` </font><br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>@color[yellow](Setting)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;@color[yellow](IntelFrameworkModulePkg/Universal/BdsDxe/BootMaint/BootMaint.c)<br>&nbsp;&nbsp;PcdSet16 &lpar;@color[red](PcdPlatformBootTimeOut),&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;  NewBmmData->BootTimeOut&rpar;;<br>&nbsp;&nbsp;</span></p>)
@snapend


@snap[north-east span-90 fragment]
<br>
<br>
<br>
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; "><br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
@color[yellow](Used)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;&nbsp;@color[yellow](OvmfPkg/Library/PlatformBootManagerLib/BdsPlatform.c)<br>&nbsp;&nbsp;&nbsp;&nbsp;Timeout = PcdGet16 &lpar;@color[red](PcdPlatformBootTimeOut)&rpar;;<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend

@snap[north-east span-90 fragment]
<br>
<p align="left" style="line-height:40%"><span style="font-size:0.9em; ">
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>@color[yellow](Modified)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.450em; font-family:Consolas; " >&nbsp;[PcdsDynamicDefault]<br>&nbsp;gEfiIntelFrameworkModulePkgTokenSpaceGuid.PcdPlatformBootTimeOut|<span style="background-color: yellow";><font color="green">`03` </font>&nbsp;</span><br>&nbsp;&nbsp;</span></p>)
@snapend





Note:

- Defined in IntelModulePkg Package .DEC
  - [PcdsDynamic]
  - 	gEfiIntelFrameworkModulePkgTokenSpaceGuid.PcdPlatformBootTimeOut|0xffff|UINT16|0x0x
- Value to use in OvmfPkgX64 Package .DSC
  - 	   gEfiIntelFrameworkModulePkgTokenSpaceGuid.PcdPlatformBootTimeOut|03
- NOTE2 Default is accually 0

- /BdsDxe/BootMaint/BootMaint.c
  -    case FORM_TIME_OUT_ID:
  -       PcdSet16 (PcdPlatformBootTimeOut, CurrentFakeNVMap->BootTimeOut);
- OvmfPkg\Library\PlatformBootManagerLib\BdsPlatform.c
  -    Timeout = PcdGet16 (PcdPlatformBootTimeOut);


---
@title[Dynamic PCD AutoGen files]
### <p align="right"><span class="gold" >Dynamic PCD AutoGen files</span></p>



@snap[north-west span-100 fragment]
<br>
<br>
<p align="left" style="line-height:60%"><span style="font-size:0.9em; ">@color[yellow](Example Module:)</span><span style="font-size:0.5em; ">&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](OvmfPkg/Library/PlatformBootManagerLib) </span><br>
<span style="font-size:0.8em; ">@color[#87E2A9](<b>Autogen.h</b>)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:40%" align="left"><span style="font-size:0.4250em; font-family:Consolas; " >&nbsp;&nbsp;@color[yellow](<sup>...</sup>)<br>&nbsp;&nbsp;&num;define _PCD_SET_MODE_16_PcdPlatformBootTimeOut&lpar;Value&rpar; \<br>&nbsp;&nbsp; LibPcdSet16&lpar;_PCD_TOKEN_PcdPlatformBootTimeOut, &lpar; @color[red](Value)  &rpar;&rpar;<br>&nbsp;&nbsp;&num;define _PCD_SET_MODE_16_S_PcdPlatformBootTimeOut&lpar;Value&rpar; \<br>&nbsp;&nbsp; LibPcdSet16S&lpar;_PCD_TOKEN_PcdPlatformBootTimeOut, &lpar; @color[red](Value)  &rpar;&rpar;<br>&nbsp;&nbsp;</span></p>)
<br>
@snapend

@snap[north-west span-100 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:60%"><span style="font-size:0.9em; "><br>@color[yellow](Example Module:)</span><span style="font-size:0.5em; ">&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](MdeModulePkg/Universal/PCD/Dxe/Pcd) </span><br>
<span style="font-size:0.8em; ">@color[#00b0f0](<b>Autogen.c</b>)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:35%" align="left"><span style="font-size:0.4250em; font-family:Consolas; " >&nbsp;&nbsp;DXE_PCD_DATABASE_INIT @color[red](gDXEPcdDbInit) = { <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](...)&nbsp;&nbsp;&nbsp;&nbsp; /&ast; LocalTokenNumberTable &ast;/&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](...)<br>&nbsp;&nbsp; offsetof&lpar;DXE_PCD_DATABASE, Init.@color[red](PcdPlatformBootTimeOut)&lowbar;&ast;<sup>1</sup>&rpar; | PCD_TYPE_DATA | <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PCD_DATUM_TYPE_UINT16,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](...)<br>&nbsp;&nbsp;&nbsp; <font color="cyan">`0x3U` </font> </font>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&sol;&ast;  <font color="red">PcdPlatformBootTimeOut</font> &lowbar;&ast;<sup>1</sup> [1] &ast;/,<br>&nbsp;&nbsp;<br>&nbsp;&nbsp;</span></p>)

@snapend



@snap[north-west span-100 fragment]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="left" style="line-height:60%"><span style="font-size:0.9em; "><br>@color[yellow](Example Module:)</span><span style="font-size:0.5em;">&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](MdeModulePkg/Universal/PCD/Dxe/Pcd) </span><br>
<span style="font-size:0.8em; ">@color[#00b0f0](<b>Autogen.c</b>)</span></p>
@box[bg-black text-white my-box-pad2  ](<p style="line-height:35%" align="left"><span style="font-size:0.4250em; font-family:Consolas; " >&nbsp;&nbsp;DXE_PCD_DATABASE_INIT <span style="background-color: white";>@color[red](gDXEPcdDbInit)</span> = { <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](...)&nbsp;&nbsp;&nbsp;&nbsp; /&ast; LocalTokenNumberTable &ast;/&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](...)<br>&nbsp;&nbsp; offsetof&lpar;DXE_PCD_DATABASE, Init.@color[red](PcdPlatformBootTimeOut)&lowbar;&ast;<sup>1</sup>&rpar; | PCD_TYPE_DATA | <br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;PCD_DATUM_TYPE_UINT16,<br>&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;@color[yellow](...)<br>&nbsp;&nbsp;&nbsp; <span style="background-color: yellow";><font color="green">`0x3U` </font>&nbsp;&nbsp;</span>&nbsp;&nbsp;&nbsp;&nbsp;&sol;&ast;  <font color="red">PcdPlatformBootTimeOut</font> &lowbar;&ast;<sup>1</sup> [1] &ast;/,<br>&nbsp;&nbsp;<br>&nbsp;&nbsp;</span></p>)

@snapend


@snap[north-east span-100 ]
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<p align="right" style="line-height:40%"><span style="font-size:0.4em; "><br><br>&ast;<sup>1</sup> GUID of PCD Variable PcdPlatformBootTimeOut </span></p>
@snapend

Note:

### Autogen files are done "behind the scenes" 

- The Module that uses the variable only has lib references to get/set the variable
- The Variable is stored in the PCD Data Base with the Driver for  the PCD manager.
- Key take away:
-   PCD act like global variables and they should only be modified at the Project level
   - Also the AutoGen files do not need to be reviewed since the work is done by the build tools.




---  
@title[Summary]
<BR>
### <p align="center"><span class="gold"   >Summary </span></p><br>
<br>
<ul style="list-style-type:none">
 <li>@fa[certificate gp-bullet-green]<span style="font-size:0.9em">&nbsp;&nbsp;Define Platform Configuration Database (PCD) and &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;explain the syntax</span> </li>
 <li>@fa[certificate gp-bullet-cyan]<span style="font-size:0.9em">&nbsp;&nbsp;Differentiate types of PCDs</span></li>
 <li>@fa[certificate gp-bullet-yellow]<span style="font-size:0.9em">&nbsp;&nbsp;Explain how changing a PCD value affects output</span> </li>
 <li>@fa[certificate gp-bullet-magenta]<span style="font-size:0.9em">&nbsp;&nbsp;Evaluate the results of a PCD value modification</span></li>
</ul>

 

---?image=assets/images/gitpitch-audience.jpg
@title[Questions]
<br>
![Questions](/assets/images/questions.JPG) 


---?image=assets/images/gitpitch-audience.jpg
@title[Logo Slide]
<br><br><br>
![Logo Slide](/assets/images/TianocoreLogo.png =10x)


---
@title[Acknowledgements]
#### <p align="center"><span class="gold"   >Acknowledgements</span></p>

```c++
/**
Redistribution and use in source (original document form) and 'compiled' forms (converted
to PDF, epub, HTML and other formats) with or without modification, are permitted provided
that the following conditions are met:

Redistributions of source code (original document form) must retain the above copyright 
notice, this list of conditions and the following disclaimer as the first lines of this 
file unmodified.

Redistributions in compiled form (transformed to other DTDs, converted to PDF, epub, HTML
and other formats) must reproduce the above copyright notice, this list of conditions and 
the following disclaimer in the documentation and/or other materials provided with the 
distribution.

THIS DOCUMENTATION IS PROVIDED BY TIANOCORE PROJECT "AS IS" AND ANY EXPRESS OR IMPLIED 
WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE IMPLIED WARRANTIES OF MERCHANTABILITY AND 
FITNESS FOR A PARTICULAR PURPOSE ARE DISCLAIMED. IN NO EVENT SHALL TIANOCORE PROJECT BE 
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR CONSEQUENTIAL DAMAGES 
(INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, 
DATA, OR PROFITS; OR BUSINESS INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, 
WHETHER IN CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE) 
ARISING IN ANY WAY OUT OF THE USE OF THIS DOCUMENTATION, EVEN IF ADVISED OF THE POSSIBILITY 
OF SUCH DAMAGE.

Copyright (c) 2018, Intel Corporation. All rights reserved.
**/

```
