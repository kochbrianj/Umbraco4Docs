#Dropdown list multiple, publish keys

`GUID 928639aa-9c73-4028-920c-1e55dbb68783`

`Retuns: Comma Separated String`

Displays a list of preset values as a list where multiple values can be selected. The value saved is a comma separeted string of prevalue IDs, the Prevalue text can be retrived using the umbraco.library.GetPreValueAsString method in XSLT or Razor

##Data Type Definition Example

![Dropdown List, Publish Keys Data Type Definition](images/Dropdown-Multiple-Publish-Keys-DataType.jpg?raw=true)

##Content Example

![Dropdown List, Publish Keys Content Example](images/Dropdown-Multiple-Publish-Keys-Content.jpg?raw=true)

##XSLT Example

	<xsl:if test="string-length($currentPage/superHeros) > 0">  
	  <xsl:variable name="items" select="umbraco.library:Split($currentPage/superHeros,',')" />  
	  <ul>  
	  <xsl:for-each select="$items//value">
	    <li>
	      <xsl:value-of select="umbraco.library:GetPreValueAsString(number(current()))"/> - <xsl:value-of select="current()"/>
	    </li>
	  </xsl:for-each>
	  </ul>    
	</xsl:if>

##Razor Example

	@{
	  if (@Model.GetProperty("superHeros").Value.Length > 0){
	    <ul>                                                        
	      @foreach(var item in @Model.GetProperty("superHeros").Value.Split(',')) { 
	       <li>@umbraco.library.GetPreValueAsString(Convert.ToInt32(item)) - @item</li>
	      }
	    </ul>                                                                                        
	  }
	}