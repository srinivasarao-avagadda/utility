@SuppressWarnings("rawtypes")
    public static HashMap<String, String> getHashMapFromJSONObject(JSONObject object) throws Exception
    {
        HashMap<String, String> toRet = null;
        try
        {
            if (object != null && object.length() > 0)
            {
                toRet = new HashMap<String, String>();
                Iterator jsonKeys = object.keys();
                while (jsonKeys.hasNext())
                {
                    String key = (String) jsonKeys.next();
                    toRet.put(key, object.getString(key));
                }
            }
        }
        catch (Exception e)
        {
            throw e;
        }
        return toRet;
    }
