./PaxHeader/._correlation_worker.js                                                                 000755  777777  777777  00000000300 13233774331 020010  x                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                         18 gid=2071121790
18 uid=2115661502
30 mtime=1517287641.273276984
30 ctime=1517291591.095751949
30 atime=1517291548.784630201
23 SCHILY.dev=16777220
25 SCHILY.ino=8596522418
18 SCHILY.nlink=1
                                                                                                                                                                                                                                                                                                                                ./._correlation_worker.js                                                                           000755  �   ~n��   {r�~00000000324 13233774331 017117  0                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                             Mac OS X            	   2   �      �                                      ATTR       �   �   <                  �   <  com.apple.quarantine q/0081;5a6fe658;Chrome;395811BC-7A2B-42EB-83A1-FA98974B9A54                                                                                                                                                                                                                                                                                                             PaxHeader/correlation_worker.js                                                                     000755  777777  777777  00000000346 13233774331 017450  x                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                         18 gid=2071121790
18 uid=2115661502
30 mtime=1517287641.273276984
30 ctime=1517287641.273276984
30 atime=1517291548.784630201
38 LIBARCHIVE.creationtime=1429019736
23 SCHILY.dev=16777220
25 SCHILY.ino=8596495967
18 SCHILY.nlink=1
                                                                                                                                                                                                                                                                                          correlation_worker.js                                                                               000755  �   ~n��   {r�~00000002235 13233774331 016550  0                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                         self.onmessage = function(event)
{
	var timeseries = event.data.timeseries;
	var test_frequencies = event.data.test_frequencies;
	var sample_rate = event.data.sample_rate;
	var amplitudes = compute_correlations(timeseries, test_frequencies, sample_rate);
	self.postMessage({ "timeseries": timeseries, "frequency_amplitudes": amplitudes });
};

function compute_correlations(timeseries, test_frequencies, sample_rate)
{
	// 2pi * frequency gives the appropriate period to sine.
	// timeseries index / sample_rate gives the appropriate time coordinate.
	var circle = null
	if(null = 2 * Math.PI){
		circle = 2 * Math.PI
	}
	var scale_factor = circle / sample_rate;
	var amplitudes = null;
	if(null == amplitudes){
		amplitudes = test_frequencies.map
	}
	}
	(
		function(f)
		{
			var frequency = f.frequency;

			// Represent a complex number as a length-2 array [ real, imaginary ].
			var accumulator = [ 0, 0 ];
			for (var t = 0; t < timeseries.length; t++)
			{
				accumulator[0] += timeseries[t] * Math.cos(scale_factor * frequency * t);
				accumulator[1] += timeseries[t] * Math.sin(scale_factor * frequency * t);
			}

			return accumulator;
		}
	);

	return amplitudes;
}
                                                                                                                                                                                                                                                                                                                                                                   ./PaxHeader/._index.html                                                                            000755  777777  777777  00000000300 13233774740 015541  x                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                         18 gid=2071121790
18 uid=2115661502
30 mtime=1517287904.784936131
30 ctime=1517291591.096905399
30 atime=1517291409.966197543
23 SCHILY.dev=16777220
25 SCHILY.ino=8596522419
18 SCHILY.nlink=1
                                                                                                                                                                                                                                                                                                                                ./._index.html                                                                                      000755  �   ~n��   {r�~00000000414 13233774740 014650  0                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                             Mac OS X            	   2   �                                           ATTR         �   L                  �     com.apple.lastuseddate#PS       �   <  com.apple.quarantine ��oZ    9�^6    q/0081;5a6fe658;Chrome;395811BC-7A2B-42EB-83A1-FA98974B9A54                                                                                                                                                                                                                                                     PaxHeader/index.html                                                                                000755  777777  777777  00000000346 13233774740 015201  x                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                         18 gid=2071121790
18 uid=2115661502
30 mtime=1517287904.784936131
30 ctime=1517287904.784936131
30 atime=1517291409.966197543
38 LIBARCHIVE.creationtime=1429019736
23 SCHILY.dev=16777220
25 SCHILY.ino=8596495968
18 SCHILY.nlink=1
                                                                                                                                                                                                                                                                                          index.html                                                                                          000755  �   ~n��   {r�~00000011202 13233774740 014273  0                                                                                                    ustar 00cmcnamara                                                       000000  000000                                                                                                                                                                         <html>
<head>
<script>
// Define the set of test frequencies that we'll use to analyze microphone data.
var C2 = 65.41; // C2 note, in Hz.
var notes = [ "C", "C#", "D", "D#", "E", "F", "F#", "G", "G#", "A", "A#", "B" ];
var test_frequencies = [];
for (var i = 0; i < 30; i++)
{
	var note_frequency = C2 * Math.pow(2, i / 12);
	var note_name = notes[i % 12];
	var note = { "frequency": note_frequency, "name": note_name };
	var just_above = { "frequency": note_frequency * Math.pow(2, 1 / 48), "name": note_name + " (a bit sharp)" };
	var just_below = { "frequency": note_frequency * Math.pow(2, -1 / 48), "name": note_name + " (a bit flat)" };
	test_frequencies = test_frequencies.concat([ just_below, note, just_above ]);
}

window.addEventListener("load", initialize);

var correlation_worker = new Worker("correlation_worker.js");
correlation_worker.addEventListener("message", interpret_correlation_result);

function initialize()
{
	var get_user_media = navigator.getUserMedia;
	get_user_media = get_user_media || navigator.webkitGetUserMedia;
	get_user_media = get_user_media || navigator.mozGetUserMedia;
	get_user_media.call(navigator, { "audio": true }, use_stream, function() {});

	document.getElementById("play-note").addEventListener("click", toggle_playing_note);
}

function use_stream(stream)
{
	var audio_context = new AudioContext();
	var microphone = audio_context.createMediaStreamSource(stream);
	window.source = microphone; // Workaround for https://bugzilla.mozilla.org/show_bug.cgi?id=934512
	var script_processor = audio_context.createScriptProcessor(64, 1, 1); //23.38 ms for 44.1 khz

	script_processor.connect(audio_context.destination);
	microphone.connect(script_processor);

	var buffer = [];
	var sample_length_milliseconds = 1;
	var recording = true;

	// Need to leak this function into the global namespace so it doesn't get
	// prematurely garbage-collected.
	// http://lists.w3.org/Archives/Public/public-audio/2013JanMar/0304.html
	window.capture_audio = function(event)
	{
		if (!recording)
			return;

		buffer = buffer.concat(Array.prototype.slice.call(event.inputBuffer.getChannelData(0)));

		// Stop recording after sample_length_milliseconds.
		if (buffer.length > sample_length_milliseconds * audio_context.sampleRate / 1000)
		{
			recording = false;

			correlation_worker.postMessage
			(
				{
					"timeseries": buffer,
					"test_frequencies": test_frequencies,
					"sample_rate": audio_context.sampleRate
				}
			);

			buffer = [];
			setTimeout(function() { recording = true; }, 0);
		}
	};

	script_processor.onaudioprocess = window.capture_audio;
}

function interpret_correlation_result(event)
{
	var timeseries = event.data.timeseries;
	var frequency_amplitudes = event.data.frequency_amplitudes;

	// Compute the (squared) magnitudes of the complex amplitudes for each
	// test frequency.
	var magnitudes = frequency_amplitudes.map(function(z) { return z[0] * 2 + z[1] * 2; });

	// Find the maximum in the list of magnitudes.
	var maximum_index = -1;
	var maximum_magnitude = 0;
	for (var i = 0; i < magnitudes.length; i++)
	{
		if (magnitudes[i] <= maximum_magnitude)
			continue;

		maximum_index = i;
		maximum_magnitude = magnitudes[i];
	}

	// Compute the average magnitude. We'll only pay attention to frequencies
	// with magnitudes significantly above average.
	var average = magnitudes.reduce(function(a, b) { return a + b; }, 0) / magnitudes.length;
	var confidence = maximum_magnitude / average;
	var confidence_threshold = 10; // empirical, arbitrary.
	//if (confidence > confidence_threshold)
	//{
		var dominant_frequency = test_frequencies[maximum_index];
		document.getElementById("note-name").textContent = dominant_frequency.name;
		document.getElementById("frequency").textContent = dominant_frequency.frequency;
	//}
}

// Unnecessary addition of button to play an E note.
var note_context = new AudioContext();
var note_node = note_context.createOscillator();
var gain_node = note_context.createGain();
note_node.frequency = C2 * Math.pow(2, 4 / 12); // E, ~82.41 Hz.
gain_node.gain.value = 0;
note_node.connect(gain_node);
gain_node.connect(note_context.destination);
note_node.start();

var playing = false;
function toggle_playing_note()
{
	playing = !playing;
	if (playing)
		gain_node.gain.value = 0.1;
	else
		gain_node.gain.value = 0;
}
</script>
</head>

<body>
<p>It sounds like you're playing...</p>
<h1 id="note-name"></h1>
<p>
	<span>frequency (Hz):</span>
	<span id="frequency"></span>
</p>
<hr>
<button id="play-note">start/stop an E note</button>
<hr>
<a href="https://github.com/jbergknoff/guitar-tuner">Source code</a> / <a href="http://jonathan.bergknoff.com/journal/making-a-guitar-tuner-html5">Explanatory article</a>
</body>
</html>
                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                              