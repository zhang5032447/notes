IMPORTANT: BY ACCESSING AND USING JETBRAINS DECOMPILER, YOU AGREE TO THE CERTAIN TERMS AND CONDITIONS SET FORTH IN THE END-USER LICENSE AGREEMENT AND QUOTED BELOW. IF YOU DO NOT AGREE WITH THESE TERMS OR CONDITIONS, DO NOT ACCESS OR USE JETBRAINS DECOMPILER.  

The Software includes decompiling functionality ("JetBrains Decompiler") that enables reproducing source code from the original binary code. Licensee acknowledges that binary code and source code might be protected by copyright and trademark laws. Before using JetBrains Decompiler, Licensee should make sure that decompilation of binary code is not prohibited by the applicable license agreement (except to the extent that Licensee may be expressly permitted under applicable law) or that Licensee has obtained permission to decompile the binary code from the copyright owner.  Using JetBrains Decompiler is entirely optional. Licensor does neither encourage nor condone the use of JetBrains Decompiler, and disclaims any liability for Licensee's use of JetBrains Decompiler in violation of applicable laws.





'com.zw.mvcframework.v2.servlet.GPDispatchServlet' is not assignable to 'javax.servlet.Servlet' 
 Inspection info: This inspection lets you spot the following problems that might occur in descriptors that are used to deploy your Web Module to a server:
References to the non-instantiable classes
References to the classes that do not extend required class
References to classes with inappropriate scope
Empty tag and attribute values
Tag and attribute values that do not match required pattern (e.g. Java Identifiers)
Tags that do not include required children tags or attributes
Tags that define objects with duplicate names



Unmapped Spring configuration files found.  Please configure Spring facet or use 'Create Default Context' to add one including all unmapped files.



Computes key.hashCode() and spreads (XORs) higher bits of hash to lower.  Because the table uses power-of-two masking, sets of hashes that vary only in bits above the current mask will always collide. (Among known examples are sets of Float keys apply a transform that spreads the impact of higher bits downward. There is a tradeoff between speed, utility, and quality of bit-spreading. Because many common sets of hashes are already reasonably distributed (so don't benefit from spreading), and because we use trees to handle large sets of collisions in bins, we just XOR some shifted bits in the cheapest possible way to reduce systematic lossage, as well as to incorporate impact of the highest bits that would otherwise never be used in index calculations because of table bounds.