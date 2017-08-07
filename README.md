
# What is subfix?

subfix is a command line tool to syncronize srt subtitles.

You can use it to fix subtitles with both constant and variable time shift.

The main philosophy behind subfix is to give it instructions for specific movie positions. You give it multiple movie positions in the format hh:mm:ss and the number of seconds that the subtitles should be shifted at that position.

Between the given positions, subfix will use linear interpolation. For example, if you tell it that it should delay the subs by 5 seconds at 30 minutes and by 15 seconds at 1 hour, it will delay them by 10 seconds at 45 minutes, The increase of the delay will be gradual between those two points.

# Usage

Requires node.js with npm

Install:

    [sudo] npm install -g subfix

The command line is

    subfix <spec> [spec, ...] < input.srt > output.srt

Where **spec** is `position+shift` or `position-shift`
 * position can be `hh:mm:ss` or `@`
 * shift is a number in seconds.

subfix will shift the subtitles at the specified position by the specified amount in seconds.

# Examples

Constantly shift the whole subtitle file by 5 seconds

    subfix @+5 < input.srt > output.srt

Start shifting by 1s at the beginning, and end with +20 seconds at the end:

    subfix @+1 @+20 < input.srt > output.srt

Start shifting by 0s at the beginning, gradually decrease to -4s at 1 hour and hold it there to the end

    subfix @+0 1:00:00-4 < input.srt > output.srt
