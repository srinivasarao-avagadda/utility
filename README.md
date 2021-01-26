public static Date getDate(String pattern, String dateStr) throws ServerException
    {
        Date toRet = null;

        try
        {
            SimpleDateFormat sdf = new SimpleDateFormat(pattern);
            toRet = sdf.parse(dateStr);
        }
        catch (Exception e)
        {
            if (e instanceof ServerException)
            {
                throw (ServerException) e;
            }
            else
            {
                throw new ServerException(e);
            }
        }
        return toRet;
    }
    
    public static long getDateMillies(String pattern, String dateStr, long defaultValue) throws ServerException
    {
        long toRet = defaultValue;
        if(dateStr != null)
        {
            Date date = getDate(pattern, dateStr);
            toRet = (date!= null ? date.getTime() : defaultValue);
        }
        return toRet;
    }
    
    public static boolean validateDate(String format, String value)
    {
        boolean toRet = false;
        Date date = null;
        try
        {
            SimpleDateFormat sdf = new SimpleDateFormat(format);
            date = sdf.parse(value);
            if (!value.equals(sdf.format(date)))
            {
                date = null;
            }
        }
        catch (ParseException ex)
        {
            logger.error(STRING_AN_ERROR_HAS_OCCURRED);
        }
        if (date != null)
        {
            toRet = true;
        }
        return toRet;
    }
