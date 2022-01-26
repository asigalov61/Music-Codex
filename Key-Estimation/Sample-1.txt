# Python 3

SCORE = [['note', 0, 2250, 0, 72, 127],
 ['note', 2625, 375, 0, 67, 127],
 ['note', 3000, 750, 0, 72, 127],
 ['note', 3750, 562, 0, 67, 127],
 ['note', 4312, 188, 0, 69, 127],
 ['note', 4500, 750, 0, 71, 127],
 ['note', 5250, 375, 0, 64, 127],
 ['note', 5625, 375, 0, 64, 127],
 ['note', 6000, 750, 0, 69, 127],
 ['note', 6750, 562, 0, 67, 127],
 ['note', 7312, 188, 0, 65, 127],
 ['note', 7500, 750, 0, 67, 127],
 ['note', 8250, 375, 0, 60, 127],
 ['note', 8625, 375, 0, 60, 127],
 ['note', 9000, 750, 0, 62, 127],
 ['note', 9750, 375, 0, 62, 127],
 ['note', 10125, 375, 0, 64, 127],
 ['note', 10500, 750, 0, 65, 127],
 ['note', 11250, 375, 0, 65, 127],
 ['note', 11625, 375, 0, 67, 127],
 ['note', 12000, 750, 0, 69, 127],
 ['note', 12750, 375, 0, 71, 127],
 ['note', 13125, 375, 0, 72, 127],
 ['note', 13500, 1125, 0, 74, 127],
 ['note', 14625, 375, 0, 67, 127],
 ['note', 15000, 750, 0, 76, 127],
 ['note', 15750, 562, 0, 74, 127],
 ['note', 16312, 188, 0, 72, 127],
 ['note', 16500, 750, 0, 74, 127],
 ['note', 17250, 375, 0, 71, 127],
 ['note', 17625, 375, 0, 67, 127],
 ['note', 18000, 750, 0, 72, 127],
 ['note', 18750, 562, 0, 71, 127],
 ['note', 19312, 188, 0, 69, 127],
 ['note', 19500, 750, 0, 71, 127],
 ['note', 20250, 375, 0, 64, 127],
 ['note', 20625, 375, 0, 64, 127],
 ['note', 21000, 750, 0, 69, 127],
 ['note', 21750, 375, 0, 67, 127],
 ['note', 22125, 375, 0, 65, 127],
 ['note', 22500, 750, 0, 67, 127],
 ['note', 23250, 375, 0, 60, 127],
 ['note', 23625, 375, 0, 60, 127],
 ['note', 24000, 750, 0, 72, 127],
 ['note', 24750, 562, 0, 71, 127],
 ['note', 25312, 188, 0, 69, 127],
 ['note', 25500, 1500, 0, 67, 127]]
 
 def SCORE_Music_Key_Estimator(SCORE):
    for S in SCORE:
        # note
        note_start_time = S[1]
        note_duration = S[2]
        note_MIDI_channel = S[3]
        note_pitch = S[4]
        note_velocity = S[5]
        # pitch class of pitch
        pc = note_pitch % 12
        if pc == 0:
            pc = 12
        # octave of pitch
        oct = int(note_pitch / 12)
        if pc < 4.5:
            oct -= 1
        # alter of pitch
        alter = pc - int(pc)
        if alter > .5 and alter < .75:
            alter = .5
        alter = int(alter * 100)
        # key estimation
        if pc < 4 and alter > 50:
            alter -= 100
            key = [oct, pc, alter]
            print(oct, pc, alter)
            break
        if pc < 4 and alter < -50:
            alter += 100
            key = [oct, pc, alter]
            print(oct, pc, alter)
            break
        if pc > 4 and alter > 50:
            alter -= 100
            key = [oct, pc, alter]
            print(oct, pc, alter)
            break
        if pc > 4 and alter < -50:
            alter += 100
            key = [oct, pc, alter]
            print(oct, pc, alter)
            break
    return key

def SCORE_Sound_Generator(SCORE, SCORE_MIDI_KEY):
    #midi = MIDIFile(1)
    #track = 0
    #channel = 0
    #time = 0
    #volume = 100
    key_root = round(SCORE_MIDI_KEY[1])
    midi_pitch = int(SCORE[0][4] % 12)
    midi_pitch -= 1
    midi_pitch += round(SCORE[0][4] / 12) - 2
    print(midi_pitch)
    #midi.addProgramChange(track, channel, time, midi_pitch)
    midi_pitch = key_root - midi_pitch

    #for S in SCORE:
    #    # note
    #    note_start_time = S[1]
    #    note_duration = S[2]
    #    note_MIDI_channel = S[3]
    #    note_pitch = S[4]
    #    note_velocity = S[5]
    #    note_end_time = note_start_time + note_duration
    #    #print(note_start_time, note_end_time, note_duration)
    #    midi.addNote(track, note_MIDI_channel, note_pitch + midi_pitch, int(note_start_time), int(note_duration), note_velocity)
    #    #midi.addNote(track, note_MIDI_channel, note_pitch, int(note_start_time), int(note_duration), note_velocity)
    #print(midi_pitch)
    #binfile = open("note2.mid", 'wb')
    #midi.writeFile(binfile)
    #binfile.close()
    
# if __name__ == "__main__":
#     SCORE = [['note', 1, 0, 0, 60, 127],
#           ['note', 1, 0, 0, 64, 127],
#           ['note', 1, 0, 0, 67, 127],
#           ['note', 1, 0, 0, 69, 127],
#           ['note', 1, 0, 0, 71, 127],
#           ['note', 1, 0, 0, 74, 127],
#           ['note', 1, 0, 0, 76, 127]]
#     SCORE_Music_Key_Estimator(SCORE)
#     SCORE_Sound_Generator(SCORE, [1, 60, 0])
