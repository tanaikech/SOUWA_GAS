/**
 * This library can perform summation of string array-elements with high speed.
 * This was effectively produced for output of CSV data from spreadsheet using GAS.
 * <h3>usage</h3>
 * <pre>
 * var sum = SOUWA.souwa(Array, Delimiter, Endcode);
 * </pre>
 * @param {Array} BaseArray Array with 1 or 2 dimentions.  e.g. Array = [a, b, c,,,,,] or Array = [[a, b, c], [d, e, f, g],,,,,]
 * @param {string} Delimiter ',' and ':' and etc.
 * @param {string} Endcode '\n' and '\r\n' and etc.
 * @return {string} Summation of array items as a string
 */
function souwa(BaseArray, Delimiter, Endcode) {
  var souwa_dat = '';
  if (BaseArray.length === 0){
    return null;
  } else if (BaseArray.length == 1) {
    return BaseArray[0].join(Delimiter) + Endcode;
  } else {
    var standardMethod = 3;
    var phi = 10;
    var omega = 0;
    var baseTheta = getSeparate_(BaseArray, standardMethod);
    var omegab = baseTheta.length - 1 + standardMethod;
    var result = new Array(baseTheta.length);
    var s1 = 0;
    var e1 = baseTheta[0];
    var theta = [];
    for (var i=0; i < baseTheta.length; i++){
      omega = omegab - i - 1;
      theta = BaseArray.slice(s1, e1);
      var theta1 = [];
      if (omega === 0 || omega < standardMethod) {
        result[i] = noDivision_(theta, Delimiter, Endcode);
      } else if (omega === 2) {
        theta1 = Division_2_(theta,  phi, Delimiter, Endcode);
        result[i] = Division_end_(theta1, phi);
      } else if (omega >= 3) {
        theta1 = Division_2_(theta,  phi, Delimiter, Endcode);
        for (var k = 0; k < (omega-2); k++){
          var theta2 = Division_3L_(theta1, phi);
          theta1 = theta2;
        }
        result[i] = Division_end_(theta1, phi);
      }
      s1 += baseTheta[i];
      e1 = s1 + baseTheta[i+1];
      theta = [];
      souwa_dat += result[i];
    }
    return souwa_dat;
  }
}


function getSeparate_(TArray, standardMethod) {
  var thetaLen = TArray.length;
  var mr = String(thetaLen).length;
  var theta_row = new Array(mr - standardMethod + 1);
  if (mr <= standardMethod) {
    theta_row[0] = thetaLen;
  } else {
    for (var i=1; i <= (mr - standardMethod); i++) {
      theta_row[i-1] = parseInt(String(thetaLen).slice(i-1,i)) * Math.pow(10, (mr - i));
    }
    theta_row[i-1] = parseInt(String(thetaLen).slice(mr - standardMethod));
  }
  return theta_row;
}


function noDivision_(theta, delimiter, ecode) {
    var string = '';
    for (var i=0; i<theta.length; i++) {
        string += theta[i].join(delimiter) + ecode;
    }
    return string;
}


function Division_2_(theta, phi, delimiter, ecode){
  var string = '';
  var AP = 0;
  var TArray = [];
  var ArrayP = 0;
  for (var i=phi; i<=(theta.length+1); i+=phi) {
    for (var j=AP; j<i; j++) {
      string += theta[j].join(delimiter) + ecode;
    }
    AP = i;
    TArray[ArrayP] = string;
    ArrayP++;
    string = '';
  }
  return TArray;
}


function Division_3L_(theta, phi){
  var string = '';
  var AP = 0;
  var TArray = [];
  var ArrayP = 0;
  for (var i=phi; i<(theta.length+1); i+=phi) {
    for (var j=AP; j<i; j++) {
      string += theta[j];
    }
    AP = i;
    TArray[ArrayP] = string;
    ArrayP++;
    string = '';
  }
  return TArray;
}


function Division_end_(theta, phi){
  var string = '';
  var result = '';
  var AP = 0;
  for (var i=phi; i<(theta.length+1); i+=phi) {
    for (var j=AP; j<i; j++) {
      string += theta[j];
    }
    AP = i;
    result += string;
    string = '';
  }
  return result;
}
