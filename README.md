# email-notification-and-attendace-loggin
%Call the Python script for face recognition

[status, cmdout] = system("python "C:\Users\admin\OneDrive\Desktop\miniproject face recognition script2.py"");

%Check for errors in Python script execution

if status ~= 0

fprintf('Error in Python scriptin5%s\n', cmdout);

return;

and

%Extract the recognized name and status from the Python output

recognized_name strtrim(cmdout); % Trim any extra spaces or newlines
%Display the recognized name for debugging purposes

disp("Recognized Name from Python: "+ recognized_name); % Debug line to print recognized name

%Check if the output indicates an unknown face

if contains(recognized_name, 'unknown') % Check for the "unknown" tag

disp('Error: Person is unknown. No email will be sent.");
else

%If recognized, log attendance and send email

%Extract recognized name from the output

name=extractBetween(recognized_name, 'recognized_name:", "valid');

if ~ isempty(name)

disp(['Recognized as:', name{1}]); % Debug line to check name

logAttendance(name (1});

sendEmail(name{1});

else

disp('Error: Could not extract name properly.');

end
end

%Function to log attendance

function log Attendance(name)

%Append the recognized name with a timestamp to a log file

logFile 'attendance_log.txt';

timestamp=datestr(now, 'yyyy-mm-dd HH:MM:SS');

logEntry = sprintf('%s-%s\n', timestamp, name);

fid = fopen(logFile, 'a');

if fid == -1

error('Unable to open log file.');
end

printf(fid, '%s', logEntry);

fclose(fid);

disp(['Attendance logged for', name]);
end

%Function to send email notification

function sendEmail(name)

%Configure email settings (replace with your email credentials)

setpref('Internet", "SMTP Server', 'smtp.gmail.com');

setpref('Internet', 'E_mail', 'newhorizoncollegetest@gmail.com");

setprefi 'Internet', 'SMTP_Username', 'newhorizoncollegetest@gmail.com");

setpref('Internet', 'SMTP_Password', 'kjzx weag ohnl vxte); % App-specific password

props=java.lang.System.getProperties;

props.setProperty('mail.smtp.auth', 'true');

ptops.setProperty('mail.smtp.starttis.enable', 'true');

%Send email

recipient = 'priyankaastikar62@gmail.com'; % Replace with the recipient's email

subject= 'Attendance Recorded';

message= sprintf('Attendance has been recorded for %s.', name);
try

sendmail(recipient, subject, message);

disp(['Email notification sent for', name]);

catch ME

disp('Failed to send email');

disp(ME.message);

end

end
