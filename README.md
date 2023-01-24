-=PBEdit 1.12=-
---------------------------------------------------------------------
a canvas-based text editor -> PureBasic only <- no external libraries

Features
    - Basic editing
    - Mouse support
    - Multicursor
    - Split view
    - Syntax highlighting
    - Indentation (none, block, automatic)
    - Autocomplete
    - Folding
    - Case correction
    - Linenumbers
    - "real" tabs or spaces
    - Undo / Redo
    - Drag & Drop
    - Find / Replace Dialog (Regular Expressions supported)
    - Bookmarks
    - Zooming
    - Repeated selections
    - Horizontal / Vertical Scrollbars (optional)
    - Customizable (via xml)
    - DPI aware (Set "Enable DPI aware executable" in compiler options)
    - Mark matching or missing keywords and brackets
    - Line continuation
    - Beautify textline after return

    v1.0.1
    added:		multilanguage support (language.cfg file)

    v1.0.2
    added:		settings file (PBEdit.xml)

    v1.0.3 		bugs fixed

    v1.0.4
    fixed:		bug in horizontal scroll (last chars of long textline not visible)
    fixed:		bug when inserting text with multiple cursors
    fixed:		missing colors in settings.xml
    fixed:		beautify procedure removed indentation when in block-mode
    changed:	redraw of cursor only if needed (avoid flickering)
    changed:	default style is black/white
    changed:	tokenizing and styling simplified
    added:		enhanced character table (use all 65535 characters instead of only 255)
    added:		if needed, set #TE_CharRange to 65536

    v1.0.5
    changed:	the cursor now has its own timer and the scroll timer is only activated if needed
    added:		french translation (thx, Mesa!)

    v1.0.6
    fixed:		a few scrolling related issues
    changed:	removed the "ID" Parameter from the Procedure "Editor_New". The return value now is a pointer to the TE_STRUCT (not the canvas ID anymore)
    added:		PostEvent to signal cursor changes (#TE_Event_Cursor) or selection changes (#TE_Event_Selection)				

    v1.0.7
    fixed:		wrong filename of default languageFile
    fixed:		faulty line continuation
    fixed:		autocomplete not showing strings starting with # or * (if flag "enableDictionary" is set to true)
    fixed:		syntax highlight issues
    fixed:		indentationLines drawn multiple times
    added:		flag "enableAutoClosingBracket": enable / disable adding of closing brackets
    added:		flag "enableZooming": enable / disable zooming
    added:		Ctrl+Tab - cycle through views

    v1.0.8
    fixed:		bug in Procedure Selection_Move that led to adding of blank lines and messed with the undo function
    fixed:		multicursor with overwrite-mode didn't work properly with multiple cursors set in same textline
    fixed:		bug in display of the AutoComplete list
    changed:	the new AutoComplete list is drawn directly on the canvas (no separate Window and ListViewGadget anymore)

    v1.0.9
    fixed:		scrolling after a textblock is unfolded
    fixed:		typo (#TE_Redraw_ChangedLined to #TE_Redraw_ChangedLines)
    fixed:		in find/replace dialog: flags #TE_Find_NoComments and #TE_Find_NoStrings not working
    fixed:		indentation bug (indentation of keywords inside comments, strings etc.)
    fixed:		scollbar bug (interaction between horizontal and vertical scrollbar didn't work properly)
    changed:	renamed PBEdit_GetFirstSelectedLineNr to PBEdit_GetCursorLineNr
    changed:	renamed PBEdit_GetFirstSelectedCharNr to PBEdit_GetCursorCharNr
    changed:	renamed PBEdit_GetLastSelectedLineNr to PBEdit_GetSelectionLineNr
    changed:	renamed PBEdit_GetLastSelectedCharNr to PBEdit_GetSelectionCharNr
    added:		PBEdit_IsGadget(ID): test if this ID is valid
    added:		PBEdit_FreeGadget(ID): remove editor and free used resources
    added:		in PBEdit_SetSelection: if LineNr < 1 clear selection
    added:		PBEdit_SelectionCharCount(ID): return the number of selected characters
    added:		Folding_ToggleAll(*te.TE_STRUCT): toggle all folds
    added:		flag "enableReadOnly": if set to true, the editor is read only (no changes of the text allowed)
    			
    v1.0.10
    fixed:		first lineNr was zero after initialization
    fixed:		bug in calculation of vertical scrollbar position
    changed:	flags in the TE_STRUCT are now a combination of "binary bit flags"
    changed:	renamed TE_CURSORSTATE\state to TE_CURSORSTATE\dragDropMode
    added:		PBEdit_SetFlag(ID, Flag, Value): set or clear the specified flag (eg. PBEdit_SetFlag(EditorID, #TE_EnableReadOnly, 1))
    added:		PBEdit_GetFlag(ID, Flag): get the specified flag
    added:		PBEdit_SetGadgetFont(ID, FontName$, FontHeight = 0, FontStyle = 0)
    added:		TE_STRUCT\foldChar (default: 1): a special character that indicates the foldstate of a newly inserted textline
    added:		horizontal autoscroll

    v1.11
    fixed:		unintended scrolling after a textblock is folded/unfolded
    fixed:		folded textblock not unfolded, when text is edited
    fixed:		numpad return key not responding in linux
    fixed:		typo "laguage" renamed to "language"
    fixed:		autocomplete scrollbar not working
    changed:	the version number now has only two parts
    changed:	CanvasGadget with flag "#PB_Canvas_Container". The ScrollBars now are added to the views CanvasGadget
    changed:	added a ContainerGadget as parent for all views
    changed:	added Procedure PBEdit_Container(ID) to get the ID of the ContainerGadget
    changed:	removed x,y,width,height from TE_STRUCT since these values can be obtained from the ContainerGadget
    changed:	#TE_SyntaxCheck to #TE_SyntaxHighlight
    changed:	#TE_Flag_... to #TE_Syntax_... and #TE_Parser_...
    changed:	TE_COLORSCHEME/defaultTextColor to TE_COLORSCHEME/defaultText
    changed:	TE_COLORSCHEME/selectedTextColor to TE_COLORSCHEME/selectedText
    changed:	the blinking of the cursor is now controlled via thread (Draw_CursorThread) - enable "Create threadsafe executable" in the compiler options!
    			if the value "cursorBlinkDelay" in the settings file is "0" the cursor is not blinking at all
    changed:	reduced unnecessary redrawing of unmodified textlines (less CPU usage when idle)
    changed:	renamed procedure Event_Resize to Editor_Resize
    changed:	improved speed of dictionary update
    changed:	improved syntax highlighting
    added:		PostEvent #TE_Event_Redraw with #TE_EventType_RedrawAll or #TE_EventType_RedrawChangedLines
    added:		Structure TE_REPEATEDSELECTION
    added:		TE_REPEATEDSELECTION\minCharacterCount: number of consecutive characters that have to be selected to highlight repeated selections
    added:		flag #TE_RepeatedSelection_WholeWord: highlight the whole word if Nr. of selected characters >= TE_REPEATEDSELECTION\minCharacterCount
    added:		flag #TE_EnableHorizontalFoldLines: if true, display a horizontal line over and under a foldable textblock
    added:		flag #TE_EnableSelection: enable/disable selecting of text
    added:		flag #TE_EnableAlwaysShowSelection: enable/disable display selection if not active gadget
    added:		flag #TE_EnableAutoClosingKeyword: enable/disable insertion of closing keyword after Tab-Key is pressed twice

    v1.12
    fixed:		jump to bookmark (F2 key) didn't jump to the correct line
    fixed:		wrong indentation when the previous textline was a split line (has line continuation)
    changed:	renamed procedure Draw_CursorThread to Cursor_Thread
    changed:	the Cursor_Thread is posting the event #TE_Event_CursorBlink to the active editor
    			the actual redrawing of the cursor takes place in the new Procedure "Event_Cursor".
    			at the moment the blink delay is set to a fixed value (500 ms).

	v1.13
	fixed:		mouse selection related issues
	fixed:		autocomplete scrollbar position
	fixed:		find/replace too slow due to permanent dictionary updates
	changed:	copy/paste with multicursor: each cursor now has it's own clipboard
	added:		Ctrl+H - replace shortcut
