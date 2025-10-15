<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Record Suspension Eligibility</title>
    <script src="https://cdn.tailwindcss.com"></script>
    <style>
        /* Custom styles to match the desired theme */
        body {
            font-family: 'Inter', sans-serif;
            background: #ffffff; /* Light gray/blue background */
            margin: 0; 
            padding: 0; 
            min-height: 100vh; 
        }
        .container-card {
            box-shadow: 0 10px 25px rgba(0, 0, 0, 0.1);
            max-width: 90%;
            margin: 2rem auto; 
            background-color: #ffffff;
            border-radius: 0.75rem; 
        }
        /* Mobile adjustment: Remove margin and make card full width on small screens */
        @media (max-width: 640px) {
            .container-card {
                max-width: 100%;
                margin: 0; 
                border-radius: 0; 
                box-shadow: none; 
            }
        }
        .section-header {
            color: #1a4d8c; /* Dark blue */
            border-bottom: 2px solid #e6f2ff;
            padding-bottom: 0.5rem;
            margin-bottom: 1.5rem;
            font-weight: 600;
        }
        
        /* ---------------------------------------------------------------------- */
        /* INPUT STYLING (Applies to date and select/dropdowns) */
        /* ---------------------------------------------------------------------- */
        
        input[type="date"], select {
            border: 1px solid #d1d5db;
            padding: 0.6rem 1rem; 
            border-radius: 0.5rem;
            width: 100%; 
            transition: border-color 0.15s ease-in-out, box-shadow 0.15s ease-in-out;
            background-color: #f9fafb;
            cursor: pointer; 
            appearance: none;
            -webkit-appearance: none;
        }
        
        input[type="date"]:focus, select:focus {
            border-color: #4f46e5; 
            box-shadow: 0 0 0 3px rgba(79, 70, 229, 0.3);
            outline: none;
        }
        
        /* Style for disabled inputs */
        input:disabled, select:disabled {
            background-color: #e5e7eb; 
            color: #9ca3af;
            cursor: not-allowed;
            opacity: 0.7;
        }

        /* Custom brown color for the Schedule 1 exception text */
        .color-brown {
            color: #6D4C41; 
        }
    </style>
</head>
<body>

    <div id="app" class="container-card p-6 md:p-10">
        
        <!-- Header: Mobile Optimized Layout -->
        <div class="flex flex-col sm:flex-row items-center sm:justify-between pb-4 mb-6 text-center sm:text-left">
            <!-- Title (Larger on mobile and takes up the top space) -->
            <h1 class="text-2xl md:text-3xl font-extrabold text-gray-900 flex-shrink-0 mb-3 sm:mb-0">
                Pardon Eligibility Checker
            </h1>
            <!-- Logo (Smaller on mobile, centered below title) -->
            <img 
                src="https://www.torontomu.ca/content/dam/law/images/TMU-Law-rgb.svg" 
                alt="Toronto Metropolitan University Law Logo" 
                class="h-10 sm:h-14 md:h-16 sm:ml-4 object-contain"
                onerror="this.onerror=null; this.src='https://placehold.co/150x40/444/FFF?text=Logo';"
            >
        </div>

        
        <!-- Disclaimer -->
        <section class="mb-8 p-4 bg-blue-50 border-l-4 border-blue-500 rounded-lg">
            <h2 class="text-xl section-header text-blue-700">Disclaimer</h2>
            <p class="text-sm text-blue-600 mb-4">This tool does not provide legal advice. Eligibility results are for informational purposes only and do not guarantee your eligibility status or whether the Parole Board of Canada will approve or deny your application. All information provided in this app is offered in good faith but may be inaccurate.</p>
            <label class="flex items-center space-x-2 cursor-pointer">
                <input type="checkbox" id="disclaimer-accepted" class="form-checkbox h-5 w-5 text-blue-500 rounded-md">
                <span class="text-sm text-gray-700 font-medium">I accept the disclaimer and wish to proceed</span>
            </label>
        </section>

        
        <!-- Input Form -->
        <section id="input-form" class="space-y-6" style="display: none;">
            <h2 class="text-xl section-header">Conviction Details</h2>

            
            <!-- Conviction Date (Date Input + Checkbox) -->
            <div class="space-y-2">
                <label for="conviction-date" class="block text-sm font-medium text-gray-700 clickable-label">Conviction Date</label>
                <div class="date-input-group space-x-4 flex items-center">
                    <!-- Standard width for dates and selects/dropdowns for alignment -->
                    <div class="w-40 md:w-52 flex-shrink-0"> 
                        <input type="date" id="conviction-date" class="w-full">
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-conv-date" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
            </div>

            
            <!-- Sentence Completion Date (Date Input + Checkbox) -->
            <div class="space-y-2">
                <label for="sentence-completion-date" class="block text-sm font-medium text-gray-700 clickable-label">Sentence Completion Date</label>
                <div class="date-input-group space-x-4 flex items-center">
                    <div class="w-40 md:w-52 flex-shrink-0">
                        <input type="date" id="sentence-completion-date" class="w-full">
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-sent-comp-date" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
                <p class="text-xs text-blue-700 mt-1">A sentence is considered complete when all fines, if any, have been paid, any probation period has ended, and any custodial term has been served.</p>
            </div>


            
            <!-- Prosecution Type (Select/Dropdown + Checkbox) -->
            <div class="space-y-2">
                <label class="block text-sm font-medium text-gray-700">Prosecution type</label>
                <div class="select-input-group space-x-4 flex items-center">
                    <div class="w-40 md:w-52 flex-shrink-0">
                        <select id="prosecution-type" class="w-full">
                            <option value="">Select an Option</option>
                            <option value="Indictment">Indictment</option>
                            <option value="Summary">Summary</option>
                        </select>
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-prosecution" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
            </div>

            
            <!-- Schedule 1 Offence (Select/Dropdown + Checkbox) -->
            <div class="space-y-2">
                <label class="block text-sm font-medium text-gray-700 flex justify-between items-center">
                    <span>Is it a Schedule 1 offence?</span>
                    <span id="schedule1-info-toggle" class="text-blue-500 hover:text-blue-700 text-xs cursor-pointer underline">What are Schedule 1 Offences?</span>
                </label>
                <div class="select-input-group space-x-4 flex items-center">
                    <div class="w-40 md:w-52 flex-shrink-0">
                        <select id="schedule1-offence" class="w-full">
                            <option value="">Select an Option</option>
                            <option value="Yes">Yes</option>
                            <option value="No">No</option>
                        </select>
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-schedule1" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
                
                <div id="schedule1-info" class="hidden mt-2 p-3 text-xs bg-blue-50 border-l-4 border-blue-500 text-blue-800 rounded">
                    <p class="mb-1">Schedule 1 generally refers to sexual offences involving children.</p>
                    
                    <p class="pt-3 mb-1 font-bold">Common Schedule 1 Offences</p>
                    <ul class="list-disc list-inside space-y-0.5 ml-4">
                        <li>Sexual interference (s. 151)</li>
                        <li>Invitation to sexual touching (s. 152)</li>
                        <li>Child pornography (s. 163.1)</li>
                        <li>Luring a child (s. 172.1)</li>
                    </ul>
                    <p class="mt-2"><a href="https://laws-lois.justice.gc.ca/eng/acts/c-47/page-4.html" target="_blank" class="text-blue-700 hover:text-blue-900 underline">See the full list here.</a></p>
                </div>
            </div>

            <!-- Serious Personal Injury Offence (SPIO) (Conditionally Visible) -->
            <div id="spio-input-group" class="space-y-2 hidden">
                <label class="block text-sm font-medium text-gray-700 flex justify-between items-center">
                    <span>Is it a Serious Personal Injury Offence (SPIO)?</span>
                    <!-- SPIO Info Toggle -->
                    <span id="spio-info-toggle" class="text-blue-500 hover:text-blue-700 text-xs cursor-pointer underline">What is a Serious Personal Injury Offence?</span>
                </label>
                <div class="select-input-group space-x-4 flex items-center">
                    <div class="w-40 md:w-52 flex-shrink-0">
                        <select id="spio-offence" class="w-full">
                            <option value="">Select an Option</option>
                            <option value="Yes">Yes</option>
                            <option value="No">No</option>
                        </select>
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-spio" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
                <!-- SPIO Info Content -->
                <div id="spio-info" class="hidden mt-2 p-3 text-xs bg-blue-50 border-l-4 border-blue-500 text-blue-800 rounded">
                    <p class="mb-2">A <b>Serious Personal Injury Offence</b> refers to:</p>
                    <div class="ml-4 space-y-1">
                        <p class="font-bold">(a) an indictable offence, other than high treason, treason, first degree murder or second degree murder, involving</p>
                        <ul class="list-disc list-inside space-y-0.5 ml-4">
                            <li>(i) the use or attempted use of violence against another person, or</li>
                            <li>(ii) conduct endangering or likely to endanger the life or safety of another person or inflicting or likely to inflict severe psychological damage on another person,</li>
                        </ul>
                        <p class="mt-1">and for which the offender may be sentenced to imprisonment for ten years or more, or</p>
                        <p class="font-bold mt-2">(b) an offence or attempt to commit an offence mentioned in section 271 (sexual assault), 272 (sexual assault with a weapon, threats to a third party or causing bodily harm) or 273 (aggravated sexual assault).</p>
                    </div>
                    <p class="mt-3">More on that here: <a href="https://laws-lois.justice.gc.ca/eng/acts/C-46/section-752.html" target="_blank" class="text-blue-700 hover:text-blue-900 underline">Criminal Code section 752.</a></p>
                </div>
            </div>

            <!-- NEW: Prison Term of 2 Years or More (Conditionally Visible) -->
            <div id="two-year-imprisonment-group" class="space-y-2 hidden">
                <label class="block text-sm font-medium text-gray-700">
                    Were sentenced to a prison term of 2 years or more?
                </label>
                <div class="select-input-group space-x-4 flex items-center">
                    <div class="w-40 md:w-52 flex-shrink-0">
                        <select id="prison-term-2yr" class="w-full">
                            <option value="">Select an Option</option>
                            <option value="Yes">Yes</option>
                            <option value="No">No</option>
                        </select>
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-prison-term-2yr" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
            </div>
            
            <!-- 3+ Convictions of 2+ Years Imprisonment (Select/Dropdown + Checkbox) -->
            <!-- This group is now conditionally displayed based on conviction date >= D3 -->
            <div id="imprisonment-convictions-group" class="space-y-2 hidden">
                <label class="block text-sm font-medium text-gray-700">Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?</label>
                <div class="select-input-group space-x-4 flex items-center">
                    <div class="w-40 md:w-52 flex-shrink-0">
                        <select id="imprisonment-convictions" class="w-full">
                            <option value="">Select an Option</option>
                            <option value="Yes">Yes</option>
                            <option value="No">No</option>
                        </select>
                    </div>
                    <label class="flex items-center space-x-2 text-sm flex-shrink-0">
                        <input type="checkbox" id="dont-know-imprisonment" class="form-checkbox h-4 w-4 text-indigo-600 rounded">
                        <span class="font-medium">I'm not sure</span>
                    </label>
                </div>
            </div>

            <!-- CHECK ELIGIBILITY BUTTON (Now same indigo color) -->
            <button id="check-eligibility-btn" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-xl transition duration-200 shadow-md mt-6">
                Check Eligibility
            </button>
        </section>

        
        <!-- Result Section -->
        <section id="result-section" class="mt-8">
            <h2 class="text-xl section-header hidden" id="result-header">Your Eligibility Status</h2>
            <div id="result-message" class="rounded-xl p-5 text-lg font-semibold">
            </div>
            
            <!-- Missing Info Details (Now placed before the email button) -->
            <div id="missing-info-details" class="mt-4 hidden p-4 bg-yellow-50 border-l-4 border-yellow-500 rounded text-sm text-yellow-800">
            </div>

            <!-- Email Button Container (Now at the very bottom) -->
            <div id="result-actions" class="mt-6 hidden">
                <button id="email-result-btn" class="w-full bg-indigo-600 hover:bg-indigo-700 text-white font-bold py-3 rounded-xl transition duration-200 shadow-md">
                    Email Results
                </button>
            </div>
        </section>

    </div>

    <script>
        // Date constants normalized to midnight UTC to ensure consistency across comparisons
        const D1 = new Date(Date.UTC(2010, 5, 29)); // June 29, 2010 (Start of transitional rules)
        const D2 = new Date(Date.UTC(2012, 2, 12)); // March 12, 2012 (End of transitional rules)
        const D3 = new Date(Date.UTC(2012, 2, 13)); // March 13, 2012 (Start of current rules)
        const TODAY = new Date();
        TODAY.setHours(0, 0, 0, 0); // Normalize today to start of the local day

        // ** Store the last calculated result for emailing **
        let latestResult = null; 

        /**
         * Generates a short, random alphanumeric reference ID.
         * @returns {string} - A random ID string (e.g., 'REF-A1B2C3D4').
         */
        function generateReferenceId() {
            // Generate a random string using base 36 (0-9, a-z), taking a 8-character slice
            const randomPart = Math.random().toString(36).substring(2, 10).toUpperCase();
            return `REF-${randomPart}`;
        }

        /**
         * Parses a date string into a Date object, normalized to midnight UTC.
         * @param {string} dateStr - Date string in YYYY-MM-DD format.
         * @returns {Date | null} - Normalized Date object or null if invalid.
         */
        function parseDate(dateStr) {
            if (!dateStr) return null;
            const parts = dateStr.split('-');
            if (parts.length !== 3) return null;
            
            const year = parseInt(parts[0], 10);
            const month = parseInt(parts[1], 10) - 1; // 0-indexed month
            const day = parseInt(parts[2], 10);

            const d = new Date(Date.UTC(year, month, day));
            return isNaN(d.getTime()) ? null : d;
        }

        /**
         * Adds a non-integer number of years to a Date object using 365.25 days/year.
         * @param {Date} date - The starting date (must be a UTC normalized Date object).
         * @param {number} years - The number of years to add.
         * @returns {Date} - The calculated future date (UTC normalized).
         */
        function addYears(date, years) {
            const newDate = new Date(date.getTime());
            // Total milliseconds to add based on 365.25 days per year
            const MS_PER_YEAR = years * 365.25 * 24 * 60 * 60 * 1000;
            newDate.setTime(newDate.getTime() + MS_PER_YEAR);
            return newDate;
        }

        /**
         * Helper function to format the calculated UTC date back to a local date string for display.
         * @param {Date} date - The calculated UTC Date object.
         * @returns {string} - Formatted date string in local time.
         */
        function formatEligibleDate(date) {
            return date.toLocaleDateString('en-US', { year: 'numeric', month: 'long', day: 'numeric', timeZone: 'UTC' });
        }
        
        const UNKNOWN_SENTINELS = ["I'm not sure", ""];

        // Embedded Ontario courthouse data (from Excel)
        

         
        const UNCLARITY_MESSAGE = "The required information to determine your eligibility date is missing. Please review the missing details below.";
        const AMBIGUITY_POSTSCRIPT = " (Your estimated timeline is provided below.)";


        /**
         * Calculates eligibility based on conviction details following the Criminal Records Act (Canada) rules.
         */
        function calculateEligibility(
            convictionDateStr, prosecutionType, schedule1Offence,
            sentenceCompletionDateStr, 
            threePlusTwoYearImprisonment, 
            spioOffence,
            imprisonmentTwoYearsOrMore // NEW ARGUMENT
        ) {
            let essentialUnknowns = [];
            let eligibleDate = null;
            let convictionDate = parseDate(convictionDateStr);
            let sentenceCompletionDate = parseDate(sentenceCompletionDateStr);
            let ambiguityMessageSuffix = ''; // Initialized here for function scope

            // ** NEW: Generate Reference ID **
            const newReferenceId = generateReferenceId();

            // Hyperlink content for the Serious Personal Injury Offence (SPIO) definition
            const criminalCodeLink = '<a href="https://laws-lois.justice.gc.ca/eng/acts/C-46/section-752.html" target="_blank" class="text-blue-600 hover:text-blue-800 underline">752 of the <i>Criminal Code</i></a>';

            // Hyperlink content for the Parole Board of Canada website (New Requirement)
            const pbcWebsiteLink = '<a href="https://www.canada.ca/en/parole-board/services/record-suspensions/applying-for-a-record-suspension.html#step6" target="_blank" class="text-blue-600 hover:text-blue-900 underline">Parole Board of Canada website</a>';

            // Helper to check for unknown values
            const isUnknown = (val) => UNKNOWN_SENTINELS.includes(val);

            // --- Helper flags for ambiguity ---
            const isConvictionDateUnknown = isUnknown(convictionDateStr) || !convictionDate;
            const isCompletionDateUnknown = isUnknown(sentenceCompletionDateStr) || !sentenceCompletionDate;
            const isProsecutionTypeUnknown = isUnknown(prosecutionType);
            const isSchedule1Unknown = isUnknown(schedule1Offence);
            const isSPIOUnknown = isUnknown(spioOffence); 
            // NEW: Imprisonment 2 years unknown flag
            const isImprisonmentTwoYearsUnknown = isUnknown(imprisonmentTwoYearsOrMore);
            
            // Note: If the 3+ convictions input is hidden, the value is forced to 'No' and is NOT considered 'Unknown' here.
            const isTwoYearImprisonmentUnknown = isUnknown(threePlusTwoYearImprisonment);

            
            // 1. Prioritized Check for Convictions on or after March 13, 2012 (D3)
            if (convictionDate && convictionDate >= D3) {
                
                // A. Schedule 1 Check (Known 'Yes')
                if (schedule1Offence === "Yes") {
                    const schedule1Message = `
                        <p class="mb-3">
                            Generally, individuals convicted of a <b>Schedule 1</b> offence are ineligible for a record suspension.
                        </p>
                        <p class="font-semibold mt-3 mb-2 text-sm">However, exceptions under Section 4(3) of the <i>Criminal Records Act</i> may apply if the convicted person:</p>
                        <ul class="list-disc list-inside space-y-2 ml-4 text-sm">
                            <li>was **not in a position of trust** or authority toward the victim;</li>
                            <li>did **not use, threaten to use or attempt to use violence, intimidation or coercion** in relation to the victim; and</li>
                            <li>was less than five years older than the victim.</li>
                        </ul>
                        <p class="mt-4 text-sm">For more information, consult the ${pbcWebsiteLink}.</p>
                    `;
                    return { status: "schedule1_exception", message: schedule1Message, eligibleDate: null, missingAnswers: [], referenceId: newReferenceId };
                }

                // B. Multiple Serious Conviction Check (Known 'Yes') -> INELIGIBLE 
                if (threePlusTwoYearImprisonment === "Yes") {
                    return {
                        status: "ineligible",
                        message: "You are not eligible for a record suspension. This is because you have three or more convictions that resulted in a sentence of imprisonment of two years or more each, and your conviction occurred on or after March 13, 2012.",
                        eligibleDate: null,
                        missingAnswers: [],
                        referenceId: newReferenceId 
                    };
                }
                
                // C. AMBIGUITY CHECK (Post-D3): If any INELIGIBILITY-RELATED factor is UNKNOWN.
                const missingIneligibilityFactor = isSchedule1Unknown || isTwoYearImprisonmentUnknown;

                if (missingIneligibilityFactor) {
                    if (isConvictionDateUnknown) essentialUnknowns.push("Conviction Date");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");

                    if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                    if (isTwoYearImprisonmentUnknown) essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");
                    
                    essentialUnknowns = Array.from(new Set(essentialUnknowns));
                    // 🟢 Updated ambiguity logic: remove redundant questions when SPIO or 2-year term = Yes
                    if (spioOffence === "Yes" || imprisonmentTwoYearsOrMore === "Yes") {
                        essentialUnknowns = essentialUnknowns.filter(q =>
                            q !== "Is it a Schedule 1 offence?" &&
                            q !== "Offence status (Serious Personal Injury Offence (SPIO))" &&
                            q !== "Were sentenced to a prison term of 2 years or more?"
                        );
                    }


                    return { 
                        status: "unclear",
                        // Standardized message applied
                        message: UNCLARITY_MESSAGE, 
                        eligibleDate: null, 
                        missingAnswers: essentialUnknowns,
                        referenceId: newReferenceId 
                    };
                }
                
                // D. Potentially Eligible (Date Unclear) Check (Only date/prosecution type are missing) - TIMELINE RANGE HERE
                if (isConvictionDateUnknown || isCompletionDateUnknown || isProsecutionTypeUnknown) {
                    if (isConvictionDateUnknown) essentialUnknowns.push("Conviction Date");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");

                    let postD3Range = "5–10 years"; // Default broad range if prosecution type is unknown

                    // Refine range based on known prosecution type
                    if (!isProsecutionTypeUnknown) {
                        if (prosecutionType === "Indictment") {
                            postD3Range = "10 years"; // Fixed 10 years for Indictment post-D3
                        } else if (prosecutionType === "Summary") {
                            postD3Range = "5 years"; // Fixed 5 years for Summary post-D3
                        }
                    }

                    // --- LOGIC: Resolve if fixed single year timeline and completion date is known (POST-D3) ---
                    const singleYearMatch = postD3Range.match(/^(\d+) years$/); 

                    if (singleYearMatch && !isCompletionDateUnknown) {
                        const fixedWaitPeriodYears = parseInt(singleYearMatch[1], 10);
                        
                        // Calculate the final date.
                        const finalEligibleDate = addYears(sentenceCompletionDate, fixedWaitPeriodYears);
                        const dateString = formatEligibleDate(finalEligibleDate);
                        
                        // Resolution message:
                        const resolutionMessage = finalEligibleDate <= TODAY 
                            ? `You are eligible to apply for a record suspension now. The waiting period was determined to be <b>${fixedWaitPeriodYears} years</b>.`
                            : `You will be eligible on ${dateString}. The required waiting period is <b>${fixedWaitPeriodYears} years</b> from your sentence completion date.`;
                        
                        // Note is needed if conviction date is still unknown.
                        let note = (isConvictionDateUnknown) ? " (Note: The conviction date remains unknown, but the fixed nature of your timeline allows for date calculation.)" : "";

                        return {
                            status: finalEligibleDate <= TODAY ? "eligible_now" : "eligible_future",
                            message: resolutionMessage + note,
                            eligibleDate: finalEligibleDate,
                            missingAnswers: [], // Resolved the date calculation
                            referenceId: newReferenceId 
                        };
                    }
                    // --- END LOGIC ---
                    
                    essentialUnknowns = Array.from(new Set(essentialUnknowns));
                    // 🟢 Updated ambiguity logic: remove redundant questions when SPIO or 2-year term = Yes
                    if (spioOffence === "Yes" || imprisonmentTwoYearsOrMore === "Yes") {
                        essentialUnknowns = essentialUnknowns.filter(q =>
                            q !== "Is it a Schedule 1 offence?" &&
                            q !== "Offence status (Serious Personal Injury Offence (SPIO))" &&
                            q !== "Were sentenced to a prison term of 2 years or more?"
                        );
                    }

                    return {
                        status: "eligible_unclear", // Retained for Post-D3 ambiguity
                        // Standardized message applied + contextual postscript
                        message: UNCLARITY_MESSAGE + AMBIGUITY_POSTSCRIPT,
                        eligibleDate: null,
                        missingAnswers: essentialUnknowns,
                        timelineRange: postD3Range,
                        referenceId: newReferenceId 
                    };
                }
                
                // If we reach here, all info is known, continue to Step 4
            } 
            
            // 2. Prioritized Check for Convictions before March 13, 2012 (Pre-D3)
            else if (convictionDate && convictionDate < D3) { 
                
                // --- SPECIAL AMBIGUITY CHECK (2010-2012 Transitional Period for Indictments with UNKNOWN Schedule 1) ---
                if (convictionDate >= D1 && convictionDate <= D2 && prosecutionType === "Indictment" && isSchedule1Unknown) {
                    
                    // NOTE: If Sch 1 is unknown, we need SPIO status, and now 2yr imprisonment status to determine the 5-10 year split.
                    let missingInfo = ["Is it a Schedule 1 offence?", "Offence status (Serious Personal Injury Offence (SPIO))", "Were sentenced to a prison term of 2 years or more?"];
                    ambiguityMessageSuffix = ''; 
                    
                    if (isCompletionDateUnknown) {
                         missingInfo.push("Sentence Completion Date (to calculate the start of the waiting period)");
                         
                         // Custom 3-point message for unknown SPIO and unknown Schedule 1
                         ambiguityMessageSuffix = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a <b>'serious personal injury offence'</b> ("SPIO"), within the meaning of ${criminalCodeLink}, or a <b>Schedule 1 offence</b>.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If the conviction was NOT a Schedule 1 offence AND NOT a SPIO: Your waiting period is <b>5 years</b>.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If the conviction was a SPIO or a Schedule 1 offence: Your waiting period is <b>10 years</b>.</span>
                                </p>
                            </div>
                        `;
                    } else {
                        // Completion Date is KNOWN
                        const date5yr = addYears(sentenceCompletionDate, 5);
                        const date10yr = addYears(sentenceCompletionDate, 10);

                        const date5yrStr = formatEligibleDate(date5yr);
                        const date10yrStr = formatEligibleDate(date10yr);

                        // Custom 3-point message for unknown SPIO and unknown Schedule 1
                        ambiguityMessageSuffix = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a <b>'serious personal injury offence'</b> (SPIO, within the meaning of ${criminalCodeLink}), or a <b>Schedule 1 offence</b>.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If the conviction was NOT a Schedule 1 offence AND NOT a SPIO: Your eligibility date is <b>${date5yrStr}</b>.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If the conviction was a SPIO or a Schedule 1 offence: Your eligibility date is <b>${date10yrStr}</b>.</span>
                                </p>
                            </div>
                        `;
                    }
                    
                    // Filter out the unknowns that are already answered
                    let missingAnswersFiltered = Array.from(new Set(missingInfo));
                    if (!isSPIOUnknown) { missingAnswersFiltered = missingAnswersFiltered.filter(i => i !== "Offence status (Serious Personal Injury Offence (SPIO))"); }
                    if (!isImprisonmentTwoYearsUnknown) { missingAnswersFiltered = missingAnswersFiltered.filter(i => i !== "Were sentenced to a prison term of 2 years or more?"); }
                    
                    return {
                        status: "likely_eligible", 
                        message: UNCLARITY_MESSAGE, 
                        eligibleDate: null, 
                        missingAnswers: missingAnswersFiltered,
                        timelineRange: "5–10 years", 
                        referenceId: newReferenceId 
                    };
                }
                
                // --- Existing SPIO/2YR Imprisonment ambiguity check (only triggers if schedule1Offence === "No") ---
                // SPIO ambiguity for transitional period D1-D2, Indictment, Sch 1 = No
                if (convictionDate >= D1 && convictionDate <= D2 && prosecutionType === "Indictment" && schedule1Offence === "No" && (isSPIOUnknown || isImprisonmentTwoYearsUnknown)) {
                    
                    let missingInfo = ["Offence status (Serious Personal Injury Offence (SPIO))", "Were sentenced to a prison term of 2 years or more?"];
                    ambiguityMessageSuffix = ''; 
                    
                    if (isCompletionDateUnknown) {
                         // Case 1: Completion Date is UNKNOWN
                         missingInfo.push("Sentence Completion Date (to calculate the start of the waiting period)");
                         
                         // The Indictment/SPIO ambiguity forces the range to 5-10 years
                         ambiguityMessageSuffix = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a <b>'serious personal injury offence'</b> (within the meaning of ${criminalCodeLink}), or if you received a sentence of <b>2 years or more</b>.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If the offence was SPIO or resulted in a sentence of 2 years or more: Your waiting period is <b>10 years</b>.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>Otherwise: Your waiting period is <b>5 years</b>.</span>
                                </p>
                            </div>
                        `;

                    } else {
                        // Case 2: Completion Date is KNOWN
                        const date5yr = addYears(sentenceCompletionDate, 5);
                        const date10yr = addYears(sentenceCompletionDate, 10);

                        const date5yrStr = formatEligibleDate(date5yr);
                        const date10yrStr = formatEligibleDate(date10yr);

                        // Use requested exact wording and formatting
                        ambiguityMessageSuffix = `
                            <p class="mt-2 text-base">
                                The eligibility date depends on whether the conviction was for a <b>'serious personal injury offence'</b> (within the meaning of ${criminalCodeLink}), or if you received a sentence of <b>2 years or more</b>.
                            </p>

                            <div class="mt-3 space-y-2 text-base ml-4">
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>If the offence was SPIO or resulted in a sentence of 2 years or more: Your eligibility date is <b>${date10yrStr}</b>.</span>
                                </p>
                                <p class="flex items-start">
                                    <span class="mr-2 font-bold leading-relaxed">-</span>
                                    <span>Otherwise: Your eligibility date is <b>${date5yrStr}</b>.</span>
                                </p>
                            </div>
                        `;
                    }
                    
                    let missingAnswersFiltered = Array.from(new Set(missingInfo));
                    if (!isSPIOUnknown) { missingAnswersFiltered = missingAnswersFiltered.filter(i => i !== "Offence status (Serious Personal Injury Offence (SPIO))"); }
                    if (!isImprisonmentTwoYearsUnknown) { missingAnswersFiltered = missingAnswersFiltered.filter(i => i !== "Were sentenced to a prison term of 2 years or more?"); }


                    return {
                        status: "likely_eligible", 
                        message: UNCLARITY_MESSAGE, 
                        eligibleDate: null,
                        missingAnswers: missingAnswersFiltered,
                        timelineRange: "5–10 years", 
                        referenceId: newReferenceId 
                    };
                }


                // Collect other unknowns for Pre-D3 
                essentialUnknowns = [];
                let range = "3–10 years"; // Default to broadest range

                // Case: Conviction Date is before D1 (Pre-June 29, 2010)
                if (convictionDate < D1) {
                    
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");

                    if (isProsecutionTypeUnknown) {
                         essentialUnknowns.push("Prosecution type");
                         range = "3–5 years"; // Unknown type before D1 is max 5 years
                    } else if (prosecutionType === "Indictment") {
                         range = "5 years";
                    } else if (prosecutionType === "Summary") {
                         range = "3 years";
                    }
                } 
                
                // Case: Conviction Date is between D1 and D3 (June 29, 2010 – March 12, 2012)
                else if (convictionDate >= D1 && convictionDate < D3) {
                    // 🟢 Updated logic (June 29 2010 → Mar 12 2012):
                    // If SPIO = Yes or 2-year term = Yes → skip Schedule 1 + the other check → wait 10 years
                    if (spioOffence === "Yes") {
                        waitPeriodYears = 10;
                        // When SPIO = Yes, we don't need Schedule 1 or the 2-year imprisonment flagged as required
                        schedule1Offence = "No";
                        imprisonmentTwoYearsOrMore = "No";
                    } else if (imprisonmentTwoYearsOrMore === "Yes") {
                        waitPeriodYears = 10;
                        // When 2-year term = Yes, we don't need Schedule 1 or SPIO flagged as required
                        schedule1Offence = "No";
                        spioOffence = "No";
                    }
    
                    
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    
                    // Schedule 1 is now flagged as essential for D1-D3 if unknown
                    if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");

                    // --- SPIO/2YR Imprisonment REQUIREMENT CHECK FOR TRANSITIONAL PERIOD (D1-D2) ---
                    // Rule: Transitional (D1-D2) AND Prosecution Type is NOT Summary (i.e., Indictment OR Unknown Type)
                    const isTransitional = convictionDate >= D1 && convictionDate <= D2;
                    const isProsecutionNotSummary = prosecutionType !== "Summary";

                    if (isTransitional && isProsecutionNotSummary) {
                        if (isSPIOUnknown) essentialUnknowns.push("Offence status (Serious Personal Injury Offence (SPIO))");
                        // NEW: Add the 2yr Imprisonment question to unknowns if applicable
                        if (isImprisonmentTwoYearsUnknown) essentialUnknowns.push("Were sentenced to a prison term of 2 years or more?");
                    }
                    // --- END SPIO/2YR CHECK ---
                    
                    // --- APPLY RANGES FOR UNKNOWNS IN D1-D3 PERIOD ---
                    
                    // Rule: Summary + Sch 1 = No (Fixed 3 years) 
                    if (prosecutionType === "Summary" && schedule1Offence === "No" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "3 years";
                    } 
                    // Rule: Summary + Sch 1 = Yes (Fixed 5 years)
                    else if (prosecutionType === "Summary" && schedule1Offence === "Yes" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "5 years";
                    }
                    // Rule: Indictment + Sch 1 = Yes (Fixed 10 years)
                    else if (prosecutionType === "Indictment" && schedule1Offence === "Yes" && !isProsecutionTypeUnknown && !isSchedule1Unknown) {
                        range = "10 years";
                    }
                    // Ambiguous Scenarios (Involving SPIO or unknown Schedule 1 status)
                    // Rule: Indictment + Sch1 Unknown -> 5-10 years 
                    else if (prosecutionType === "Indictment" && isSchedule1Unknown && !isProsecutionTypeUnknown) {
                        range = "5–10 years";
                    }
                    // Rule: Summary + Sch 1 = Unknown -> 3-5 years
                    else if (prosecutionType === "Summary" && isSchedule1Unknown && !isProsecutionTypeUnknown) {
                        range = "3–5 years";
                    }
                    
                    // Rule: Unknown Prosecution & Schedule 1 = No -> 3-10 years 
                    else if (isProsecutionTypeUnknown && (schedule1Offence === "No" || isSchedule1Unknown)) {
                        range = "3–10 years";
                    }
                    // Rule: Unknown Prosecution & Schedule 1 = Yes -> 5-10 years
                    else if (isProsecutionTypeUnknown && schedule1Offence === "Yes") {
                        range = "5–10 years";
                    }

                    // ** LOGIC: Override Unknown Prosecution Type if SPIO or 2YR Imprisonment is known YES and we are D1-D2 **
                    if (isTransitional && (spioOffence === "Yes" || imprisonmentTwoYearsOrMore === "Yes") && isProsecutionTypeUnknown) {
                        // SPIO='Yes' or 2Yr Imprisonment='Yes' forces 10 years, making prosecution type irrelevant for the wait period.
                        // Filter out Prosecution type from unknowns if it was added.
                        essentialUnknowns = essentialUnknowns.filter(item => item !== "Prosecution type");
                        
                        // If only completion date is left as unknown, this is now a fixed 10-year period ambiguity
                        if (essentialUnknowns.length > 0) {
                            range = "10 years";
                            ambiguityMessageSuffix = '<p class="mt-2 text-base">Since the conviction is a Serious Personal Injury Offence (SPIO) or resulted in a sentence of 2 years or more, the eligibility waiting period is fixed at <b>10 years</b> from your sentence completion date.</p>';
                        } else {
                            // If completion date is known, and SPIO/2YR is Yes, we can skip to Step 4 with a known 10-year wait.
                            prosecutionType = "Indictment"; 
                            schedule1Offence = "No"; 
                            // Fall through to Step 4
                        }
                    }
                }
                
                // If there are unknowns, return the 'likely_eligible' status with the determined range
                if (essentialUnknowns.length > 0) {
                    
                    // --- LOGIC: Resolve if fixed single year timeline and completion date is known (PRE-D3) ---
                    const singleYearMatch = range.match(/^(\d+) years$/); 

                    if (singleYearMatch && !isCompletionDateUnknown) {
                        const fixedWaitPeriodYears = parseInt(singleYearMatch[1], 10);
                        
                        // Calculate the final date.
                        const finalEligibleDate = addYears(sentenceCompletionDate, fixedWaitPeriodYears);
                        const dateString = formatEligibleDate(finalEligibleDate);
                        
                        // Resolution message:
                        const resolutionMessage = finalEligibleDate <= TODAY 
                            ? `You are eligible to apply for a record suspension now. The waiting period was determined to be <b>${fixedWaitPeriodYears} years</b>.`
                            : `You will be eligible on ${dateString}. The required waiting period is <b>${fixedWaitPeriodYears} years</b> from your sentence completion date.`;
                        
                        // Note is needed if conviction date is still unknown.
                        let note = (isConvictionDateUnknown) ? " (Note: The conviction date remains unknown, but the fixed nature of your timeline allows for date calculation.)" : "";

                        return {
                            status: finalEligibleDate <= TODAY ? "eligible_now" : "eligible_future",
                            message: resolutionMessage + note,
                            eligibleDate: finalEligibleDate,
                            missingAnswers: essentialUnknowns, // Still include the unknowns for transparency
                            referenceId: newReferenceId 
                        };
                    }
                    // --- END LOGIC ---

                     return { 
                        status: "likely_eligible", 
                        message: UNCLARITY_MESSAGE, 
                        eligibleDate: null, 
                        missingAnswers: Array.from(new Set(essentialUnknowns)),
                        timelineRange: range,
                        referenceId: newReferenceId 
                    };
                }
                
                // If we reach here, all info is known and we continue to Step 4
            } 
            
            // 3. Fallback if Conviction Date is UNKNOWN (Conviction Date is 'I'm not sure' or empty)
            else if (isConvictionDateUnknown) {

                // A. Check for known ineligibility (Sch 1 is Yes) 
                if (schedule1Offence === "Yes" && !isSchedule1Unknown) {
                    
                    essentialUnknowns = [];
                    essentialUnknowns.push("Conviction Date");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    // Only add the 3+ convictions question as an unknown if the user saw it (i.e., if Conviction Date was NOT 'I'm not sure' before)
                    if (threePlusTwoYearImprisonment === "I'm not sure") essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");
                    
                    return {
                        status: "unclear",
                        // Standardized message applied
                        message: UNCLARITY_MESSAGE,
                        eligibleDate: null,
                        missingAnswers: Array.from(new Set(essentialUnknowns)),
                        referenceId: newReferenceId 
                    };
                    
                }

                // B. Check for conditional ineligibility (3+ Convictions)
                if (threePlusTwoYearImprisonment === "Yes" && !isTwoYearImprisonmentUnknown) {
                    // If 3+ is YES, but Conviction Date is UNKNOWN, we must return UNCLEAR, not INELIGIBLE.
                    essentialUnknowns = [];
                    essentialUnknowns.push("Conviction Date");
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    
                    return {
                        status: "unclear",
                        // Standardized message applied
                        message: UNCLARITY_MESSAGE,
                        eligibleDate: null,
                        missingAnswers: Array.from(new Set(essentialUnknowns)),
                        referenceId: newReferenceId 
                    };
                }


                // C. If we reach here: Conviction Date is Unknown, Sch 1='No', and 3+ Conv='No'. Likely Eligible but Timeline Unknown.
                if (schedule1Offence === "No" && threePlusTwoYearImprisonment === "No") {
                    
                    let range = "3–10 years"; // Default to broadest range (Conviction Date is unknown, so 3-10 years is possible)
                    
                    // Collect remaining unknowns
                    if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                    if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                    // Conviction Date is the main reason we are here, so add it
                    essentialUnknowns.push("Conviction Date");
                    
                    // Customize range based on known non-date factors:
                    if (prosecutionType === "Indictment" && !isProsecutionTypeUnknown) {
                        // If Indictment is KNOWN, the min wait time is 5, max is 10 (pre-D1 vs post-D3)
                        range = "5–10 years";
                    } else if (prosecutionType === "Summary" && !isProsecutionTypeUnknown) {
                        // If Summary is KNOWN, the min wait time is 3, max is 5 (pre-D1 vs post-D3)
                        range = "3–5 years";
                    }

                    // --- LOGIC: Resolve if fixed single year timeline and completion date is known (UNKNOWN CONVICTION DATE) ---
                    const singleYearMatch = range.match(/^(\d+) years$/); 
                    
                    // Check if: 1. Range is fixed (e.g., '5 years'), 2. Completion Date is known (not unknown)
                    if (singleYearMatch && !isCompletionDateUnknown) {
                        const fixedWaitPeriodYears = parseInt(singleYearMatch[1], 10);
                        
                        // Calculate the final date.
                        const finalEligibleDate = addYears(sentenceCompletionDate, fixedWaitPeriodYears);
                        const dateString = formatEligibleDate(finalEligibleDate);
                        
                        // Resolution message:
                        const resolutionMessage = finalEligibleDate <= TODAY 
                            ? `You are eligible to apply for a record suspension now. The waiting period was determined to be <b>${fixedWaitPeriodYears} years</b>.`
                            : `You will be eligible on ${dateString}. The required waiting period is <b>${fixedWaitPeriodYears} years</b> from your sentence completion date.`;
                        
                        // Note is mandatory here since conviction date is definitely unknown.
                        let note = " (Note: The conviction date remains unknown, but the fixed nature of your timeline allows for date calculation.)";

                        return {
                            status: finalEligibleDate <= TODAY ? "eligible_now" : "eligible_future",
                            message: resolutionMessage + note,
                            eligibleDate: finalEligibleDate,
                            // The only true unknown remaining is Conviction Date, but we don't need it for calculation
                            missingAnswers: [], 
                            referenceId: newReferenceId 
                        };
                    }
                    // --- END LOGIC ---
                    
                    // Uses 'eligible_unclear' here because the Conviction Date is unknown and could be post-D3.
                    return {
                        status: "eligible_unclear",
                        // Standardized message applied + contextual postscript
                        message: UNCLARITY_MESSAGE + AMBIGUITY_POSTSCRIPT,
                        eligibleDate: null,
                        missingAnswers: Array.from(new Set(essentialUnknowns)),
                        timelineRange: range,
                        referenceId: newReferenceId 
                    };
                }
                
                // D. Fallback (If other factors are missing, e.g., Sch1 or 3+ is 'I'm not sure')
                essentialUnknowns = [];
                if (isConvictionDateUnknown) essentialUnknowns.push("Conviction Date");
                if (isCompletionDateUnknown) essentialUnknowns.push("Sentence Completion Date");
                if (isProsecutionTypeUnknown) essentialUnknowns.push("Prosecution type");
                if (isSchedule1Unknown) essentialUnknowns.push("Is it a Schedule 1 offence?");
                if (isTwoYearImprisonmentUnknown) essentialUnknowns.push("Have you had 3 or more convictions resulting in imprisonment of 2 years or more each?");


                    return { 
                    status: "unclear", 
                    // Standardized message applied
                    message: UNCLARITY_MESSAGE, 
                    eligibleDate: null, 
                    missingAnswers: Array.from(new Set(essentialUnknowns)),
                    referenceId: newReferenceId 
                };
            }


            // 4. Calculate Wait Period (All required info is known and no ambiguity was found)
            let waitPeriodYears = 0;

            if (convictionDate < D1) {
                // Before June 29, 2010 (Old Rules) - Fixed 3 or 5 years.
                waitPeriodYears = (prosecutionType === "Indictment") ? 5 : 3;
            } else if (convictionDate >= D1 && convictionDate <= D2) {
                // Between June 29, 2010 and March 12, 2012 (Transitional Rules)
                
                if (schedule1Offence === "Yes") {
                    // Schedule 1 conviction is 10 years if Indictment, 5 years if Summary
                    waitPeriodYears = (prosecutionType === "Indictment") ? 10 : 5; 
                } else if (prosecutionType === "Summary") { 
                    // Summary and Not Schedule 1 (3 years - using old rule)
                    waitPeriodYears = 3;
                } else {
                    // Indictment and Not Schedule 1
                    // CRITICAL: We use the *known* SPIO status OR the 2YR Imprisonment status to decide 5 or 10 years.
                    waitPeriodYears = (spioOffence === "Yes" || imprisonmentTwoYearsOrMore === "Yes") ? 10 : 5; 
                }
            } else if (convictionDate >= D3) {
                // On or after March 13, 2012 (Current Rules) - CONFIRMED LOGIC
                waitPeriodYears = (prosecutionType === "Indictment") ? 10 : 5;
            } else {
                // Fallback for unhandled date
                return { status: "unclear", message: UNCLARITY_MESSAGE, eligibleDate: null, missingAnswers: ["Conviction Date"], referenceId: newReferenceId };
            }

            // 5. Final Status Determination
            eligibleDate = addYears(sentenceCompletionDate, waitPeriodYears);

            if (eligibleDate <= TODAY) {
                return {
                    status: "eligible_now",
                    message: `You are eligible to apply for a record suspension now. The waiting period was determined to be <b>${waitPeriodYears} years</b>.`,
                    eligibleDate: eligibleDate,
                    missingAnswers: [],
                    referenceId: newReferenceId 
                };
            } else {
                const dateString = formatEligibleDate(eligibleDate);
                return {
                    status: "eligible_future",
                    message: `You will be eligible on ${dateString}. The required waiting period is <b>${waitPeriodYears} years</b> from your sentence completion date.`,
                    eligibleDate: eligibleDate,
                    missingAnswers: [],
                    referenceId: newReferenceId 
                };
            }
        }

        // --- UI Logic and Event Handlers ---

        const elements = {
            disclaimerCheckbox: document.getElementById('disclaimer-accepted'),
            inputForm: document.getElementById('input-form'),
            checkEligibilityBtn: document.getElementById('check-eligibility-btn'),
            resultSection: document.getElementById('result-section'),
            resultHeader: document.getElementById('result-header'),
            resultMessage: document.getElementById('result-message'),
            missingInfoDetails: document.getElementById('missing-info-details'),
            
            // NEW: Email Action Elements
            resultActions: document.getElementById('result-actions'),
            emailResultBtn: document.getElementById('email-result-btn'),

            // Dates
            convictionDate: document.getElementById('conviction-date'),
            dontKnowConvDate: document.getElementById('dont-know-conv-date'),
            sentenceCompletionDate: document.getElementById('sentence-completion-date'),
            dontKnowSentCompDate: document.getElementById('dont-know-sent-comp-date'),
            
            // Prosecution Type
            prosecutionType: document.getElementById('prosecution-type'),
            dontKnowProsecution: document.getElementById('dont-know-prosecution'),
            
            // Schedule 1 Offence
            schedule1Offence: document.getElementById('schedule1-offence'),
            dontKnowSchedule1: document.getElementById('dont-know-schedule1'),

            // SPIO Offence Elements
            spioInputGroup: document.getElementById('spio-input-group'),
            spioOffence: document.getElementById('spio-offence'),
            dontKnowSPIO: document.getElementById('dont-know-spio'),
            spioInfoToggle: document.getElementById('spio-info-toggle'), 
            spioInfo: document.getElementById('spio-info'),           
            
            // NEW: 2-Year Imprisonment Elements
            twoYearImprisonmentGroup: document.getElementById('two-year-imprisonment-group'),
            prisonTerm2yr: document.getElementById('prison-term-2yr'),
            dontKnowPrisonTerm2yr: document.getElementById('dont-know-prison-term-2yr'),

            // 3+ Convictions
            imprisonmentConvictionsGroup: document.getElementById('imprisonment-convictions-group'), 
            imprisonmentConvictions: document.getElementById('imprisonment-convictions'),
            dontKnowImprisonment: document.getElementById('dont-know-imprisonment'),
            
            // Info Toggle
            schedule1InfoToggle: document.getElementById('schedule1-info-toggle'),
            schedule1Info: document.getElementById('schedule1-info'),
        };

        /**
         * Generic function to handle the 'I'm not sure' checkbox logic for select elements.
         * Disables and resets the select element when the 'I'm not sure' checkbox is checked.
         */
        function handleUnknownSelect(checkboxElement, selectElement) {
            if (checkboxElement.checked) {
                selectElement.disabled = true;
                selectElement.value = ''; // Clear selection
            } else {
                selectElement.disabled = false;
            }
        }

        /**
         * Generic function to get the value for a select/checkbox group.
         * @param {HTMLElement} selectElement - The <select> element.
         * @param {HTMLElement} notSureCheckboxElement - The 'I'm not sure' checkbox.
         * @returns {string} - 'I'm not sure', the selected dropdown value, or empty string.
         */
        function getSelectCheckboxValue(selectElement, notSureCheckboxElement) {
            // If disabled, its value is being controlled by the app based on other inputs.
            if (selectElement.disabled) {
                return selectElement.value;
            }
            if (notSureCheckboxElement.checked) return "I'm not sure";
            return selectElement.value;
        }


        // Conditional display for "I'm not sure" handling across all inputs
        function updateConditionalInputs() {
            // Conviction Date
            handleUnknownSelect(elements.dontKnowConvDate, elements.convictionDate);

            // Sentence Completion Date
            handleUnknownSelect(elements.dontKnowSentCompDate, elements.sentenceCompletionDate);
            
            // Prosecution Type
            handleUnknownSelect(elements.dontKnowProsecution, elements.prosecutionType);
            
            // Schedule 1 Offence
            handleUnknownSelect(elements.dontKnowSchedule1, elements.schedule1Offence);
            
            
            // Get current conviction date for conditional checks
            const convDateStr = elements.convictionDate.value;
            const convictionDate = parseDate(convDateStr);
            const prosecutionTypeVal = getSelectCheckboxValue(elements.prosecutionType, elements.dontKnowProsecution);

            
            // --- SPIO and 2-Year Imprisonment Conditional Display Logic ---
            const isTransitional = convictionDate && convictionDate >= D1 && convictionDate <= D2;
            const isProsecutionNotSummary = prosecutionTypeVal !== "Summary";
            const isConditionalSectionVisible = isTransitional && isProsecutionNotSummary;


            if (isConditionalSectionVisible) {
                // SPIO Group
                elements.spioInputGroup.classList.remove('hidden');
                handleUnknownSelect(elements.dontKnowSPIO, elements.spioOffence); 
                
                // NEW: 2-Year Imprisonment Group (Same logic as SPIO)
                elements.twoYearImprisonmentGroup.classList.remove('hidden');
                handleUnknownSelect(elements.dontKnowPrisonTerm2yr, elements.prisonTerm2yr); 

            } else {
                // SPIO Group
                elements.spioInputGroup.classList.add('hidden');
                elements.spioOffence.value = '';
                elements.spioOffence.disabled = false;
                elements.dontKnowSPIO.checked = false;
                
                // NEW: 2-Year Imprisonment Group
                elements.twoYearImprisonmentGroup.classList.add('hidden');
                elements.prisonTerm2yr.value = '';
                elements.prisonTerm2yr.disabled = false;
                elements.dontKnowPrisonTerm2yr.checked = false;
            }

            // --- Imprisonment Convictions Conditional Display Logic ---
            // Only visible if the conviction date is on or after March 13, 2012 (D3)
            const isPostD3 = convictionDate && convictionDate >= D3;

            if (isPostD3) {
                elements.imprisonmentConvictionsGroup.classList.remove('hidden');
                
                // If the element was hidden (disabled=true) or had the system-forced 'No' value, reset it.
                if (elements.imprisonmentConvictions.disabled || elements.imprisonmentConvictions.value === 'No') {
                    elements.imprisonmentConvictions.value = ''; // Force "Select an Option"
                    elements.dontKnowImprisonment.checked = false; // Ensure 'I'm not sure' is off for a fresh choice
                }

                // If it becomes visible, re-enable and handle based on its specific checkbox
                elements.imprisonmentConvictions.disabled = false;
                handleUnknownSelect(elements.dontKnowImprisonment, elements.imprisonmentConvictions); 
            } else {
                // If not post-D3, hide the group
                elements.imprisonmentConvictionsGroup.classList.add('hidden');
                // Crucially, reset the app-controlled values to ensure calculation logic is correct for pre-D3 (rule does not apply)
                elements.imprisonmentConvictions.value = 'No';
                elements.imprisonmentConvictions.disabled = true; // Disable to signal it's system-controlled
                elements.dontKnowImprisonment.checked = false; // Reset checkbox
            }
        }

        // Event listener setup
        elements.dontKnowConvDate.addEventListener('change', updateConditionalInputs);
        elements.dontKnowSentCompDate.addEventListener('change', updateConditionalInputs);
        elements.dontKnowProsecution.addEventListener('change', updateConditionalInputs);
        elements.dontKnowSchedule1.addEventListener('change', updateConditionalInputs);
        
        // Listen to the date picker itself for the main conditional logic
        elements.convictionDate.addEventListener('change', () => { 
            if (elements.convictionDate.value) elements.dontKnowConvDate.checked = false; 
            updateConditionalInputs(); 
        });

        // NEW: 2-Year Imprisonment Listeners
        elements.prisonTerm2yr.addEventListener('change', () => { if (elements.prisonTerm2yr.value) elements.dontKnowPrisonTerm2yr.checked = false; updateConditionalInputs(); });
        elements.dontKnowPrisonTerm2yr.addEventListener('change', updateConditionalInputs);

        // 3+ Convictions Listeners 
        elements.imprisonmentConvictions.addEventListener('change', () => { 
             if (elements.imprisonmentConvictions.value) elements.dontKnowImprisonment.checked = false; 
             updateConditionalInputs(); 
        });
        elements.dontKnowImprisonment.addEventListener('change', updateConditionalInputs);


        // Other listeners
        elements.dontKnowSPIO.addEventListener('change', updateConditionalInputs);
        elements.spioOffence.addEventListener('change', () => { if (elements.spioOffence.value) elements.dontKnowSPIO.checked = false; updateConditionalInputs(); });
        elements.sentenceCompletionDate.addEventListener('change', () => { if (elements.sentenceCompletionDate.value) elements.dontKnowSentCompDate.checked = false; updateConditionalInputs(); });
        elements.prosecutionType.addEventListener('change', () => { 
            if (elements.prosecutionType.value) elements.dontKnowProsecution.checked = false; 
            updateConditionalInputs(); 
        });
        elements.schedule1Offence.addEventListener('change', () => { if (elements.schedule1Offence.value) elements.dontKnowSchedule1.checked = false; updateConditionalInputs(); });
        

        // Toggle Schedule 1 Info
        elements.schedule1InfoToggle.addEventListener('click', () => {
            elements.schedule1Info.classList.toggle('hidden');
            elements.schedule1InfoToggle.innerHTML = elements.schedule1Info.classList.contains('hidden') ? '<u>What are Schedule 1 Offences?</u>' : '[x] Close';
        });
        
        // Toggle SPIO Info
        if (elements.spioInfoToggle) {
             elements.spioInfoToggle.addEventListener('click', () => {
                elements.spioInfo.classList.toggle('hidden');
                elements.spioInfoToggle.innerHTML = elements.spioInfo.classList.contains('hidden') ? '<u>What is a Serious Personal Injury Offence?</u>' : '[x] Close';
             });
             // Initial setup for the link text
             elements.spioInfoToggle.innerHTML = '<u>What is a Serious Personal Injury Offence?</u>'; 
        }

        window.addEventListener('load', () => {
             updateConditionalInputs();
             // Initial setup for link texts
             elements.schedule1InfoToggle.innerHTML = '<u>What are Schedule 1 Offences?</u>'; 
        }); 

        // Event listener for disclaimer
        elements.disclaimerCheckbox.addEventListener('change', () => {
            elements.inputForm.style.display = elements.disclaimerCheckbox.checked ? 'block' : 'none';
            // Clear results and hide actions on uncheck
            elements.resultHeader.classList.add('hidden');
            elements.resultMessage.innerHTML = '';
            elements.missingInfoDetails.classList.add('hidden');
            elements.resultActions.classList.add('hidden');
        });

        // Event listener for eligibility check
        elements.checkEligibilityBtn.addEventListener('click', () => {
            if (!elements.disclaimerCheckbox.checked) {
                // Generates a reference ID even for error/unclear state
                displayResult({ status: 'unclear', message: UNCLARITY_MESSAGE, eligibleDate: null, missingAnswers: ["Disclaimer Acceptance"], referenceId: generateReferenceId() });
                return;
            }

            // Get date strings, prioritizing 'I'm not sure' checkbox over the date picker value
            const convictionDateInputStr = getSelectCheckboxValue(elements.convictionDate, elements.dontKnowConvDate);
            const sentenceCompletionDateInputStr = getSelectCheckboxValue(elements.sentenceCompletionDate, elements.dontKnowSentCompDate);
            
            // Get values from the new select/checkbox groups
            const prosecutionTypeVal = getSelectCheckboxValue(elements.prosecutionType, elements.dontKnowProsecution);
            const schedule1OffenceVal = getSelectCheckboxValue(elements.schedule1Offence, elements.dontKnowSchedule1);
            // Retrieve SPIO value
            const spioOffenceVal = getSelectCheckboxValue(elements.spioOffence, elements.dontKnowSPIO);
            // NEW: Retrieve 2-Year Imprisonment value
            const imprisonmentTwoYearsOrMoreVal = getSelectCheckboxValue(elements.prisonTerm2yr, elements.dontKnowPrisonTerm2yr);
            const threePlusTwoYearImprisonmentVal = getSelectCheckboxValue(elements.imprisonmentConvictions, elements.dontKnowImprisonment);
            
            // Call calculateEligibility with the updated argument list (7 arguments now)
            const result = calculateEligibility(
                convictionDateInputStr,
                prosecutionTypeVal,
                schedule1OffenceVal,
                sentenceCompletionDateInputStr,
                threePlusTwoYearImprisonmentVal,
                spioOffenceVal,
                imprisonmentTwoYearsOrMoreVal // NEW ARGUMENT
            );

            displayResult(result);
        });

        /**
         * Renders the result object to the UI, applying custom styling for Schedule 1 exception,
         * and sets the latest result for emailing.
         */
        
        
        // --- Courthouse dropdown population and display helpers (JSON-based) ---
        async function populateCourthouseDropdown() {
            const select = document.getElementById('courthouse-select');
            const details = document.getElementById('courthouse-details');
            if (!select || !details) return;
            select.innerHTML = '<option value=\"\">Select a location</option>';
            try {
                const response = await fetch('ontario_courts.json');
                const data = await response.json();
                data.forEach((c, idx) => {
                    const opt = document.createElement('option');
                    opt.value = idx;
                    opt.textContent = c.Location || ('Location ' + (idx + 1));
                    select.appendChild(opt);
                });
                select.addEventListener('change', () => {
                    const val = select.value;
                    if (val === '') {
                        details.classList.add('hidden');
                        details.innerHTML = '';
                        return;
                    }
                    const item = data[parseInt(val, 10)];
                    if (!item) return;
                    details.classList.remove('hidden');
                    details.innerHTML = `
                        <div class="font-bold text-gray-900 text-base">${item.Location}</div>
                        <div class="text-sm text-gray-700 mt-1">${item.Address}</div>
                        <div class="text-sm text-gray-700 mt-1">Phone: ${item.Phone}</div>
                        <div class="mt-2 text-sm"><a href="https://www.ontario.ca/locations/courts" target="_blank" class="text-blue-700 hover:underline">View all Ontario courts</a></div>
                    `;
                });
            } catch (err) {
                console.error('Error loading ontario_courts.json:', err);
                details.classList.remove('hidden');
                details.innerHTML = '<div class="text-red-700 text-sm">Unable to load courthouse list. Please visit <a href="https://www.ontario.ca/locations/courts" target="_blank" class="text-blue-700 hover:underline">Ontario Courts</a>.</div>';
            }
        }


        function displayResult(result) {
            // Set the latest result globally for the email function to access
            latestResult = result;

            elements.resultHeader.classList.remove('hidden');
            elements.missingInfoDetails.classList.add('hidden');
            elements.resultActions.classList.remove('hidden'); // SHOW THE EMAIL BUTTON CONTAINER
            
            // Reset base classes, adding shadow and transition back
            elements.resultMessage.className = 'rounded-xl p-5 text-lg font-semibold mt-4 shadow-lg transition-all duration-300';
            let htmlContent = '';
            let styleClasses = '';
            let missingListHTML = '';
            
            // HTML for courthouse contact info 
            const courthouseContactHtml = `
                <div class="mt-4 font-bold">You can obtain this information from the courthouse where you were convicted:</div>
                <div id="courthouse-contact-widget" class="mt-3 p-3 bg-white rounded-lg shadow-sm">
                    <label for="courthouse-select" class="block text-sm font-medium text-gray-700 mb-2">Find your courthouse contact info</label>
                    <select id="courthouse-select" class="w-full border rounded p-2 mb-3">
                        <option value="">Select a location</option>
                    </select>
                    <div id="courthouse-details" class="hidden p-3 bg-gray-50 rounded text-sm text-gray-800"></div>
                    <p class="mt-3 text-sm"><a href="https://www.ontario.ca/locations/courts" target="_blank" class="text-blue-700 hover:underline">View all Ontario courts</a></p>
                </div>
            `;
            
            let refIdFooter = ''; // Footer element for the Reference ID

            // Determine classes and content based on status
            switch (result.status) {
                case 'eligible_now':
                    styleClasses = 'bg-green-100 border-l-8 border-green-600 text-green-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-green-600">🎉</span><h3 class="font-bold text-xl"><b>Eligible Now!</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    // Reference ID color scheme
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-green-300 text-right text-xs font-mono tracking-widest text-green-600">
                        ${result.referenceId}
                    </p>`;
                    break;

                case 'eligible_future':
                    styleClasses = 'bg-green-100 border-l-8 border-green-600 text-green-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-green-600">&#9202;</span><h3 class="font-bold text-xl"><b>Eligible in the Future</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    // Reference ID color scheme
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-green-300 text-right text-xs font-mono tracking-widest text-green-600">
                        ${result.referenceId}
                    </p>`;
                    break;

                case 'ineligible':
                    styleClasses = 'bg-red-100 border-l-8 border-red-600 text-red-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-red-600">&#10060;</span><h3 class="font-bold text-xl"><b>Ineligible</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    // Reference ID color scheme
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-red-300 text-right text-xs font-mono tracking-widest text-red-600">
                        ${result.referenceId}
                    </p>`;
                    break;

                case 'schedule1_exception':
                    styleClasses = 'bg-yellow-100 border-l-8 border-amber-600'; 
                    htmlContent = `
                        <div class="flex items-center space-x-3">
                            <span class="text-3xl text-amber-600">⚠️</span>
                            <h3 class="font-bold text-xl text-black"><b>Schedule 1 Offence — Possible Exception</b></h3>
                        </div>
                        <div class="color-brown mt-2">
                            ${result.message}
                        </div>
                    `;
                    // Reference ID color scheme
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-amber-300 text-right text-xs font-mono tracking-widest text-amber-600">
                        ${result.referenceId}
                    </p>`;
                    break;
                
                case 'likely_eligible':
                    // UPDATED TO GREEN THEME
                    styleClasses = 'bg-green-100 border-l-8 border-green-600 text-green-800'; 
                    // CRITICAL: The result.message will now be UNCLARITY_MESSAGE only.
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-green-600">&#9989;</span><h3 class="font-bold text-xl"><b>Likely Eligible</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
                    if (result.timelineRange) {
                        // Updated bg-color for the timeline box
                        htmlContent += `<p class="mt-3 text-sm font-bold bg-green-200 p-2 rounded-lg inline-block">Potential eligibility timeline: ${result.timelineRange}</p>`;
                    }

                    elements.missingInfoDetails.classList.remove('hidden');
                    missingListHTML = result.missingAnswers.map(ans => `<li>${ans}</li>`).join('');
                    
                    elements.missingInfoDetails.innerHTML = `<p class="font-bold">To determine your exact eligibility date, please provide answers for:</p><ul class="list-disc list-inside mt-2 ml-4">${missingListHTML}</ul><p class="mt-2">Please try to locate this information before applying, as the date of eligibility depends on it.</p>` + courthouseContactHtml;
                    // Initialize courthouse dropdown widget when missing info box is shown
                    if (document.getElementById('courthouse-select')) { populateCourthouseDropdown(); }

                    
                    // Reference ID color scheme (Updated to green)
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-green-300 text-right text-xs font-mono tracking-widest text-green-600">
                        ${result.referenceId}
                    </p>`;
                    break;

                case 'eligible_unclear':
                    styleClasses = 'bg-blue-100 border-l-8 border-blue-600 text-blue-800'; 
                    // UPDATED TEXT HERE
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-blue-600">&#63;</span><h3 class="font-bold text-xl"><b>Eligibility Unclear</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
                    if (result.timelineRange) {
                        htmlContent += `<p class="mt-3 text-sm font-bold bg-blue-200 p-2 rounded-lg inline-block">Potential eligibility timeline: ${result.timelineRange}</p>`;
                    }

                    elements.missingInfoDetails.classList.remove('hidden');
                    missingListHTML = result.missingAnswers.map(ans => `<li>${ans}</li>`).join('');
                    
                    elements.missingInfoDetails.innerHTML = `<p class="font-bold">To determine your exact eligibility date, please provide answers for:</p><ul class="list-disc list-inside mt-2 ml-4">${missingListHTML}</ul><p class="mt-2">Please try to locate this information before applying, as the date of eligibility depends on it.</p>` + courthouseContactHtml;
                    // Initialize courthouse dropdown widget when missing info box is shown
                    if (document.getElementById('courthouse-select')) { populateCourthouseDropdown(); }

                    
                    // Reference ID color scheme
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-blue-300 text-right text-xs font-mono tracking-widest text-blue-600">
                        ${result.referenceId}
                    </p>`;
                    break;

                case 'unclear':
                default:
                    styleClasses = 'bg-blue-100 border-l-8 border-blue-600 text-blue-800';
                    htmlContent = `<div class="flex items-center space-x-3"><span class="text-3xl text-blue-600">&#63;</span><h3 class="font-bold text-xl"><b>Eligibility Unclear</b></h3></div><p class="mt-2 text-base">${result.message}</p>`;
                    
                    if (result.missingAnswers.length > 0) {
                        elements.missingInfoDetails.classList.remove('hidden');
                        missingListHTML = result.missingAnswers.map(ans => `<li>${ans}</li>`).join('');
                        
                        elements.missingInfoDetails.innerHTML = `<p class="font-bold">To get a clearer assessment, please provide answers for:</p><ul class="list-disc list-inside mt-2 ml-4">${missingListHTML}</ul><p class="mt-2">The timing and definitive status of your eligibility depends on these details.</p>` + courthouseContactHtml;
                    // Initialize courthouse dropdown widget when missing info box is shown
                    if (document.getElementById('courthouse-select')) { populateCourthouseDropdown(); }

                    }

                    // Reference ID color scheme
                    refIdFooter = `<p class="mt-4 pt-2 border-t border-blue-300 text-right text-xs font-mono tracking-widest text-blue-600">
                        ${result.referenceId}
                    </p>`;
                    break;
            }

            elements.resultMessage.classList.add(...styleClasses.split(' '));
            elements.resultMessage.innerHTML = htmlContent + refIdFooter; // ** APPEND Reference ID at the bottom **
        }


        /**
         * Gathers the eligibility data and triggers a mailto: link to draft an email.
         */
        function emailResults() {
            if (!latestResult) {
                console.error("No results to email. Button should not be visible.");
                return;
            }
            
            // Determine the status text based on the result status for the subject
            let statusTitle = "Eligibility Check Result";
            let statusDisplay = "";

            switch (latestResult.status) {
                case 'eligible_now':
                    statusTitle = "Eligible for Record Suspension (NOW)";
                    statusDisplay = "Status: Eligible Now!";
                    break;
                case 'eligible_future':
                    statusTitle = "Eligible for Record Suspension (Future Date)";
                    statusDisplay = `Status: Eligible in the Future (${formatEligibleDate(latestResult.eligibleDate)})`;
                    break;
                case 'ineligible':
                    statusTitle = "Ineligible for Record Suspension";
                    statusDisplay = "Status: Ineligible";
                    break;
                case 'schedule1_exception':
                    statusTitle = "Schedule 1 Offence - Possible Exception";
                    statusDisplay = "Status: Schedule 1 Offence — Possible Exception";
                    break;
                case 'likely_eligible':
                    statusTitle = "Likely Eligible for Record Suspension (Pre-March 2012 Conviction)";
                    statusDisplay = "Status: Likely Eligible";
                    break;
                case 'eligible_unclear':
                    statusTitle = "Eligibility Unclear (Post-March 2012 Ambiguity)";
                    statusDisplay = "Status: Eligibility Unclear";
                    break;
                case 'unclear':
                default:
                    statusTitle = "Eligibility Unclear";
                    statusDisplay = "Status: Eligibility Unclear";
                    break;
            }
            
            // Get the final result message text content (stripping HTML)
            const resultMessageDiv = document.getElementById('result-message');
            // Clone and strip HTML for a clean text version
            const rawContent = resultMessageDiv.cloneNode(true);
            
            // Remove the reference ID footer and HTML elements (like links, strong tags) for a clean text body
            const footer = rawContent.querySelector('p:last-child');
            if (footer) footer.remove();

            // Replace HTML with line breaks and clean up spacing
            let bodyMessage = rawContent.textContent.replace(/\n\s*\n/g, '\n\n').trim();
            bodyMessage = bodyMessage.replace(/([.?!])\s*([A-Z])/g, '$1\n\n$2');

            // --- START: LOGIC TO INCLUDE MISSING INFORMATION ---
            let missingInfoText = '';
            const missingInfoDiv = document.getElementById('missing-info-details');
            
            // Check if the missing info panel is currently visible
            if (missingInfoDiv && !missingInfoDiv.classList.contains('hidden')) {
                
                // Extract the list of missing items and format them with bullets
                const listItems = Array.from(missingInfoDiv.querySelectorAll('li')).map(li => `  - ${li.textContent.trim()}`).join('\n');
                
                // Include the link/source information if present (to obtain the missing details)
                let contactInfo = '';
                if (missingInfoDiv.textContent.includes('courthouse')) {
                     contactInfo = '\n\nSource for missing information: You can obtain this information from the courthouse where you were convicted.';
                }
                
                missingInfoText = `

--- Required Information for a Final Assessment ---
To determine your exact status or eligibility date, please provide answers for:

${listItems}${contactInfo}

Please try to locate this information before proceeding with an application.
`;
            }
            // --- END: LOGIC ---

            // Construct the final email body
            let finalBody = `
Dear Applicant,

Thank you for using the Pardon Eligibility Checker. Here is a summary of your results:

${statusDisplay}
Reference ID: ${latestResult.referenceId}

--- Detailed Message ---
${bodyMessage}

${missingInfoText}

---
Disclaimer: This tool does not constitute legal advice and is provided for informational purposes only.
`;
            
            const subject = encodeURIComponent(`Pardon Eligibility: ${statusTitle}`);
            const body = encodeURIComponent(finalBody.trim());
            
            // Trigger the mailto link to open the user's email client
            const mailtoLink = `mailto:?subject=${subject}&body=${body}`;

            window.location.href = mailtoLink;
        }

        // Add event listener for the new button
        elements.emailResultBtn.addEventListener('click', emailResults);

    </script>
</body>
</html>
