# ONEDeFi Deployment Guide for Render

This guide will walk you through deploying your ONEDeFi application on Render.

## Prerequisites

1. **GitHub Repository**: Your code should be in a GitHub repository
2. **Render Account**: Sign up at [render.com](https://render.com)
3. **Environment Variables**: Prepare any API keys or configuration values

## Method 1: Automatic Deployment (Recommended)

### Step 1: Connect Repository to Render

1. Go to [Render Dashboard](https://dashboard.render.com)
2. Click "New +" button
3. Select "Blueprint"
4. Connect your GitHub account if not already connected
5. Select your repository containing the ONEDeFi code

### Step 2: Configure Blueprint

Render will automatically detect the `render.yaml` file and configure:
- **Web Service**: `onedefi-server`
- **Database**: `onedefi-db` (PostgreSQL)
- **Environment Variables**: Auto-configured from render.yaml

### Step 3: Deploy

1. Click "Apply" to start the deployment
2. Render will:
   - Create the PostgreSQL database
   - Build and deploy the web service
   - Link the database to the web service
   - Generate a secure session secret

### Step 4: Access Your Application

Once deployment is complete, you'll get a URL like:
```
https://onedefi-server.onrender.com
```

## Method 2: Manual Deployment

### Step 1: Create PostgreSQL Database

1. Go to Render Dashboard
2. Click "New +" → "PostgreSQL"
3. Configure:
   - **Name**: `onedefi-db`
   - **Database**: `onedefi`
   - **User**: `onedefi_user`
   - **Plan**: Free
4. Click "Create Database"

### Step 2: Create Web Service

1. Go to Render Dashboard
2. Click "New +" → "Web Service"
3. Connect your GitHub repository
4. Configure the service:

**Basic Settings:**
- **Name**: `onedefi-server`
- **Environment**: `Python`
- **Region**: Choose closest to your users
- **Branch**: `main` (or your default branch)
- **Root Directory**: Leave empty (if code is in root)

**Build & Deploy:**
- **Build Command**: `pip install -r requirements.txt`
- **Start Command**: `gunicorn main:app --bind 0.0.0.0:$PORT`

**Environment Variables:**
- `PYTHON_VERSION`: `3.11.0`
- `DATABASE_URL`: Link to your PostgreSQL database
- `SESSION_SECRET`: Generate a random string
- `FLASK_ENV`: `production`
- `FLASK_DEBUG`: `false`

### Step 3: Deploy

1. Click "Create Web Service"
2. Render will build and deploy your application
3. Monitor the build logs for any issues

## Environment Variables

### Required Variables

| Variable | Description | Example |
|----------|-------------|---------|
| `DATABASE_URL` | PostgreSQL connection string | `postgresql://user:pass@host:port/db` |
| `SESSION_SECRET` | Flask session secret | `your-secret-key-here` |

### Optional Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `FLASK_ENV` | Flask environment | `production` |
| `FLASK_DEBUG` | Debug mode | `false` |
| `PORT` | Port number | Auto-assigned by Render |

## Troubleshooting

### Common Issues

1. **Build Failures**
   - Check that all dependencies are in `requirements.txt`
   - Ensure Python version compatibility
   - Review build logs for specific errors

2. **Database Connection Issues**
   - Verify `DATABASE_URL` is correctly set
   - Check database is created and accessible
   - Ensure PostgreSQL extension is enabled

3. **Application Crashes**
   - Check application logs in Render dashboard
   - Verify all environment variables are set
   - Test locally before deploying

### Debugging Steps

1. **Check Build Logs**
   - Go to your service in Render dashboard
   - Click "Logs" tab
   - Look for error messages during build

2. **Check Runtime Logs**
   - Monitor application logs for runtime errors
   - Check for missing environment variables
   - Verify database connections

3. **Test Locally**
   - Run `python main.py` locally
   - Test with PostgreSQL database
   - Verify all features work

## Performance Optimization

### For Production

1. **Database Optimization**
   - Use connection pooling
   - Implement proper indexing
   - Monitor query performance

2. **Application Optimization**
   - Enable caching where appropriate
   - Optimize static file serving
   - Implement proper error handling

3. **Monitoring**
   - Set up health checks
   - Monitor response times
   - Track error rates

## Security Considerations

1. **Environment Variables**
   - Never commit secrets to Git
   - Use Render's environment variable management
   - Rotate secrets regularly

2. **Database Security**
   - Use strong passwords
   - Enable SSL connections
   - Restrict access to necessary IPs

3. **Application Security**
   - Keep dependencies updated
   - Implement proper authentication
   - Use HTTPS (automatic on Render)

## Scaling

### Free Tier Limitations

- **Web Service**: 750 hours/month
- **Database**: 90 days, then $7/month
- **Bandwidth**: 100GB/month

### Upgrading

1. **Web Service**: Upgrade to paid plan for more resources
2. **Database**: Upgrade for longer retention and better performance
3. **Custom Domain**: Add your own domain name

## Support

- **Render Documentation**: [docs.render.com](https://docs.render.com)
- **Community**: [Render Community](https://community.render.com)
- **Status**: [status.render.com](https://status.render.com)

## Next Steps

After successful deployment:

1. **Test All Features**: Verify all functionality works
2. **Set Up Monitoring**: Configure alerts and monitoring
3. **Custom Domain**: Add your own domain (optional)
4. **SSL Certificate**: Automatic with Render
5. **Backup Strategy**: Set up database backups

---

**Note**: This deployment guide is specifically for Render. For other platforms, refer to their respective documentation.
