<!DOCTYPE html>
<html>

<head>
  
<script src="plugins/jspsych.js"></script>
<script src="plugins/jspsych-html-keyboard-response.js"></script>
<script src="plugins/jspsych-html-button-response.js"></script>
<link rel="stylesheet" href="plugins/jspsych.css"></link>
<style>
.stimulus { font-size: 35px; }
</style>
</head>

<script>
	var timeline = [];

        /*subject registration*/
	var subject_id = jsPsych.randomization.randomID(3);
	jsPsych.data.addProperties({
	subject: subject_id,
	});

        /*set up the welcome block*/
        var firstwelcome = {
	type: "html-keyboard-response",
	stimulus: "Welcome to our experiment. Please press the spacebar to read the instructions."
        };
	timeline.push(firstwelcome);

        /*set up the instructions block*/
        var instructions = {
	type: "html-keyboard-response",
	stimulus: "<p>In this task, you will see a series of English sentences on the screen.</p><p>One sentence will be presented at a time on the screen.</p><p>Your job is to read each sentence aloud as naturally as possible.</p><p>After reading each sentence aloud, please press the spacebar to see the next sentence.</p><p>Please press the spacebar if you are ready to begin the task.</p>"
        };
	timeline.push(instructions);

        /*set up the stimuli block*/
	var stimuli = [
	{sentence: 'I said yield again.'},
	{sentence: 'I said yip again.'},
	{sentence: 'I said yes again.'},
	{sentence: 'I said yap again.'},
	{sentence: 'I said you again.'},
	{sentence: 'I said yolk again.'},
	{sentence: 'I said yacht again.'},
	{sentence: 'I said weed again.'},
	{sentence: 'I said win again.'},
	{sentence: 'I said wet again.'},
	{sentence: 'I said woo again.'},
	{sentence: 'I said wood again.'},
	{sentence: 'I said woke again.'},
	{sentence: 'I said wall again.'},
	{sentence: 'I said heed again.'},
	{sentence: 'I said hid again.'},
	{sentence: 'I said hayed again.'},
	{sentence: 'I said head again.'},
	{sentence: 'I said had again.'},
	{sentence: 'I said hud again.'},
	{sentence: 'I said hide again.'},
	{sentence: 'I said who\'d again.'},
	{sentence: 'I said hood again.'},
	{sentence: 'I said hoed again.'},
	{sentence: 'I said hod again.'}

	];

        /*set up the task block*/
	var task = {
	timeline_variables: stimuli,
	randomize_order: true,
	repetitions: 2,
	timeline: [
	{
        type: 'html-keyboard-response',
        stimulus: '<p class="stimulus"></p>',
        trial_duration: 1000,
        post_trial_gap: 0
	},
	{
        type: 'html-keyboard-response',
        stimulus: function(){ return "<p class='stimulus'>"+jsPsych.timelineVariable('sentence', true)+"</p>"; },
        post_trial_gap: 0,
	}
	]
	}
	timeline.push(task);

        /*set up the end block*/
	var endexpa = {
	type: "html-keyboard-response",
	stimulus: "<p>The experiment is over.</p><p>Please press the spacebar.</p>"
        };
	timeline.push(endexpa);

        /*set up the end block*/
	var endexpb = {
	type: 'html-button-response',
	stimulus: "<p>Please do the followings.</p><p>Please stop the recording, and download the wav file created.</p><p>After saving the audio file, please press the button below and download the experiment text file.</p><p>Thank you so much for your time.</p>",
	choices: ['Create the experiment text file.']
        };
	timeline.push(endexpb);

	jsPsych.init({
	timeline: timeline,
	on_finish: function() {
	jsPsych.data.get().localSave('csv','mydata.txt');
	},
	default_iti: 250
	});

</script>

</html>
