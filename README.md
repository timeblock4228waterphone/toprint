# toprint
to print
oct 2 to fix the 9 system because the supid 3 by 4 grid
fix both of it


iiii

// ==========================================
// ARROW TIME OPERATING SYSTEM (LINE-FREE v2)
// Purpose: Convert 24h clock into two pure spatial vectors
// ==========================================

FUNCTION TranslateTimeToGlyphs(input_hour, input_minute):

    // STEP 1: INITIAL DATA SANITIZATION (Page 5)
    IF input_hour < 0 OR input_hour > 23 OR input_minute < 0 OR input_minute > 59:
        RETURN "AMBIGUOUS"
    END IF


    // STEP 2: THE ROBUST "ROUND DOWN" RULE (Page 5, 6)
    // Round minute down to the nearest 5-minute block
    target_minute = input_minute - (input_minute MOD 5)
    target_hour = input_hour


    // STEP 3: RUN THE GROUP AND VALUE EQUATIONS (Page 3)
    // Hour equation: Hour = 6 * (GroupA - 1) + ValueB
    // Minute equation: Minute = 30 * (GroupC - 1) + 5 * ValueD
    
    // Calculate Hour Indices
    GroupA = FLOOR(target_hour / 6) + 1
    ValueB = target_hour MOD 6
    IF ValueB == 0:
        ValueB = 6           // 00 displays handle end of cycle (Page 6)
        GroupA = GroupA - 1
    END IF

    // Calculate Minute Indices
    GroupC = FLOOR(target_minute / 30) + 1
    ValueD = (target_minute MOD 30) / 5
    IF ValueD == 0 AND target_minute > 0:
        ValueD = 6
        GroupC = GroupC - 1
    END IF


    // STEP 4: DEFINE VECTOR DIRECTION CODES (Page 3)
    // 1=↖, 2=↑, 3=↗, 4=↙, 5=↓, 6=↘
    DIRECTION_ARRAY = ["↖", "↑", "↗", "↙", "↓", "↘"]
    
    // Left Position: Determine Hour Direction
    Hour_Direction = DIRECTION_ARRAY[ValueB - 1]


    // STEP 5: OVERRIDE FOR THE NEW 45-MIN CARDINAL GEAR (User Updated)
    // Override ValueD if exact 15/30/45/00 cardinal marks hit
    IF target_minute == 0:
        Minute_Direction = "↑"    // Up arrow is 00
    ELSE IF target_minute == 15:
        Minute_Direction = "→"    // Right arrow is 15
    ELSE IF target_minute == 30:
        Minute_Direction = "↓"    // Down arrow is 30
    ELSE IF target_minute == 45:
        Minute_Direction = "←"    // Left arrow is 45
    ELSE
        // Fallback to baseline index mapping if not a pure 45-min marker
        Minute_Direction = DIRECTION_ARRAY[ValueD - 1]
    END IF


    // STEP 6: COMBO INTO THE LINE-FREE GLYPH LAYOUT (User Updated)
    // Enforce horizontal presentation: Left = Hour, Right = Minute
    // Remove the boundary line entirely to strip cognitive clutter
    Final_Layout = Hour_Direction + "     " + Minute_Direction

//start with 1:30 to 6:45 adding 45 minute interval. 

//show the result for it
   
    RETURN Final_Layout


END FUNCTION

