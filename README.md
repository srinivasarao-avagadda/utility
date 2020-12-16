https://javadeveloperzone.com/java-8/parse-large-json-file-jackson-example/


 public static Object safeGetJSONObject(String path, JSONObject jObj) {
        Object retVal = new JSONObject();
        try {
            JSONObject jTemp = jObj;

            if (jObj != null) {
                String[] propPath = path.split("\\."); // split takes a regex, so to demarcate using period, you have to escape it

                if (propPath.length > 0) {
                    int i;
                    for (i = 0; i < propPath.length - 1; i++) {
                        if (jTemp != null) {
                            Object jTempObj = jTemp.opt(propPath[i]);
                            if (!(JSONObject.NULL).equals(jTempObj)) {
                                if (jTempObj instanceof JSONArray && propPath.length > i) {
                                    int indexPos = getIntValue(propPath[i + 1], 0);
                                    if (indexPos >= 0) {
                                        Object tmpObj = ((JSONArray) jTempObj).get(indexPos);
                                        if (tmpObj instanceof String) {
                                            jTemp = new JSONObject((String) tmpObj);
                                        } else {
                                            jTemp = (JSONObject) tmpObj;
                                        }
                                    }
                                    i += 1;
                                } else {
                                    jTemp = (JSONObject) jTempObj;
                                }
                            } else {
                                jTemp = null;
                            }
                        } else {
                            break;
                        }
                    }

                    if (jTemp != null) {
                        if (i == propPath.length) {
                            retVal = jTemp;
                        } else {
                            retVal = jTemp.opt(propPath[propPath.length - 1]);
                        }
                    }
                } else {
                    System.out.println("Got bogus call for " + path);
                }
            }
        } catch (JSONException t) {
            // do nothing
        }

        return retVal;
    }

    public static String safeGetJSONProperty(String path, JSONObject jObj) {
        Object toRet = safeGetJSONObject(path, jObj);
        return toRet != null ? toRet.toString() : null;
    }
