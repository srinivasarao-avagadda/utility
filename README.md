public static List<String> getJSONArrayAsList(JSONArray jArray) throws Exception
    {
        List<String> toRet = null;
        if (jArray != null)
        {
            toRet = new ArrayList<String>();
            for (int i = 0; i < jArray.length(); i++)
            {
                toRet.add(jArray.getString(i));
            }
        }
        return toRet;
    }
