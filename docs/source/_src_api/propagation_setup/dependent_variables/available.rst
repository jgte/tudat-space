.. _available_dependent_variables:

Available Dependent Variables
#############################

All variables are saved in SI units. Dependent variables can be added to the propagation settings by first defining a list of desired dependent variables.


.. code-block:: python
      
    dependent_variables_to_save = [
        propagation_setup.dependent_variable.total_acceleration( "Delfi-C3" ),
        propagation_setup.dependent_variable.keplerian_state( "Delfi-C3", "Earth" ),
        propagation_setup.dependent_variable.latitude( "Delfi-C3", "Earth" ),
        propagation_setup.dependent_variable.longitude( "Delfi-C3", "Earth" )
    ]

Then, add this list to the propagating settings.

.. code-block:: python

    propagator_settings = propagation_setup.propagator.translational(
	    central_bodies,
	    acceleration_models,
	    bodies_to_propagate,
	    initial_state,
	    simulation_end_epoch,
	    output_variables = dependent_variables_to_save
    )

After the dynamics simulator has been called, the dependent variable history can be retrieved as:

.. code-block:: python

	dependent_variables = dynamics_simulator.dependent_variable_history

.. note::

	Dependent variables can be saved for each (celestial) body, as long as it has been defined in the environment.

- **Mach Number**

	Mach number in atmosphere. Requires an aerodynamic acceleration to be acting on the vehicle.

	.. code-block:: python

		 propagation_setup.dependent_variable.mach_number( "Spacecraft", "Earth" )

- **Altitude** 

	Altitude above body exerting aerodynamic acceleration. Requires an aerodynamic acceleration to be acting on the vehicle.

	.. code-block:: python

		propagation_setup.dependent_variable.altitude( "Spacecraft", "Earth" )

- **Airspeed**
	
	Airspeed in atmosphere of body exerting aerodynamic acceleration. Requires an aerodynamic acceleration to be acting on the vehicle.

	.. code-block:: python

		propagation_setup.dependent_variable.airspeed( "Spacecraft", "Earth" )

- **Density**

	Local density in atmosphere of body exerting aerodynamic acceleration (at position of body undergoing acceleration). Requires an aerodynamic acceleration to be acting on the vehicle. 

	.. code-block:: python

		propagation_setup.dependent_variable.density( "Spacecraft", "Earth" )

- **Relative Position**

	Vector position of a body with respect to a second body (between centers of mass).

	.. code-block:: python

		propagation_setup.dependent_variable.relative_position( "Spacecraft", "Earth" )

- **Relative Distance**

	Scalar distance of a body with respect to a second body (between centers of mass). 

	.. code-block:: python

		propagation_setup.dependent_variable.relative_distance( "Spacecraft", "Earth" )

- **Relative Velocity**

	Vector velocity of a body with respect to a second body (between centers of mass).

	.. code-block:: python

		propagation_setup.dependent_variable.relative_velocity( "Spacecraft", "Earth" )

- **Relative Speed**

	Scalar velocity of a body with respect to a second body (between centers of mass).

	.. code-block:: python

		propagation_setup.dependent_variable.relative_speed( "Spacecraft", "Earth" )

- **Keplerian State**

	.. code-block:: python

		propagation_setup.dependent_variable.keplerian_state( "Spacecraft", "Earth" )


	Returns six columns:
	1: Semi-major Axis. 2: Eccentricity. 3: Inclination. 4: Argument of Periapsis. 5. Right Ascension of the Ascending Node. 6: True Anomaly.
	
- **Modified Equinoctial State**
	
	.. code-block:: python
	
		propagation_setup.dependent_variable.modified_equinoctial_state( "Spacecraft", "Earth" )
		
	Returns six columns, where the elements are in the following order: 
	
	1. :math:`p` (Semilatus rectum)
	2. :math:`f = e \cdot \cos\left(\omega + I\Omega\right)`
	3. :math:`g = e \cdot \sin\left(\omega + I\Omega\right)`
	4. :math:`h = \arctan\left(\frac{i}{2}\right) \cdot \cos \Omega`
	5. :math:`k = \arctan\left(\frac{i}{2}\right) \cdot \sin \Omega`
	6. :math:`L = \omega + I\Omega + \theta` (True longitude)
	
	For more information on modified equinoctial elements, see for instance `this paper <https://arc.aiaa.org/doi/pdf/10.2514/1.32237>`_.

- **Single Acceleration**

	.. code-block:: python

		propagation_setup.dependent_variable.single_acceleration( 
			propagation_setup.acceleration.point_mass_gravity_type, "Spacecraft", "Earth" )

	Here is a list with the :ref:`acceleration_types`.

- **Single Acceleration Norm**

	.. code-block:: python

		propagation_setup.dependent_variable.single_acceleration_norm( 
			propagation_setup.acceleration.point_mass_gravity_type, "Spacecraft", "Earth" )

	Here is a list with the :ref:`acceleration_types`.

- **Spherical Harmonic Terms Acceleration**

	.. code-block:: python

		spherical_harmonic_terms = [ (2,0), (2,1), (2,2) ]
		propagation_setup.dependent_variable.spherical_harmonic_terms_acceleration( "Spacecraft", "Earth", spherical_harmonic_terms )

	The entries in the ``spherical_harmonic_terms`` define the (degree, order) pairs of which the contribution to the spherical harmonic acceleration is to be retrieved.

- **Spherical Harmonic Terms Acceleration Norm**

	.. code-block:: python

		spherical_harmonic_terms = [ (2,0), (2,1), (2,2) ]
		propagation_setup.dependent_variable.spherical_harmonic_terms_acceleration_norm( "Spacecraft", "Earth", spherical_harmonic_terms )

	The entries in the ``spherical_harmonic_terms`` define the (degree, order) pairs of which the norm of the contribution to the spherical harmonic acceleration is to be retrieved.

- **Total Acceleration**

	.. code-block:: python

		propagation_setup.dependent_variable.total_acceleration( "Spacecraft" )
		
	Returns the total acceleration (in vector form) acting upon the specified body.

- **Total Acceleration Norm**

	.. code-block:: python

		propagation_setup.dependent_variable.total_acceleration_norm( "Spacecraft" )
		
	Returns the norm of the total acceleration acting upon the specified body, i.e. its scalar value.

- **Aerodynamic Force Coefficients**

	Aerodynamic force coefficients for the specified body.

	.. code-block:: python

		propagation_setup.dependent_variable.aerodynamic_force_coefficients( "Spacecraft" )

- **Aerodynamic Moment Coefficients**

	Aerodynamic moment coefficients for the specified body.

	.. code-block:: python

		propagation_setup.dependent_variable.aerodynamic_moment_coefficients( "Spacecraft" )

- **Latitude**

	Latitude of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.latitude( "Spacecraft", "Earth" )
		
- **Geodetic Latitude**

	Geodetic latitude of the first body w.r.t. the second body.
	
	.. code-block:: python

		propagation_setup.dependent_variable.geodetic_latitude( "Spacecraft", "Earth" )

- **Longitude**

	Longitude of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.longitude( "Spacecraft", "Earth" )

- **Heading Angle**

	Heading of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.heading_angle( "Spacecraft", "Earth" )

- **Flight Path Angle**

	Flight path angle of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.flight_path_angle( "Spacecraft", "Earth" )
		
- **Angle of Attack**

	Angle of attack of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.angle_of_attack( "Spacecraft", "Earth" )
	
- **Sideslip Angle**

	Sideslip angle of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.sideslip_angle( "Spacecraft", "Earth" )
		
- **Bank Angle**

	Bank angle of the first body w.r.t. the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.bank_angle( "Spacecraft", "Earth" )
		
- **Control Surface Deflection**

	Deflection of specified control surface on associated body. The name of the control surface is the second argument and needs to match the names given in the control surface setup.

	.. code-block:: python

		propagation_setup.dependent_variable.control_surface_deflection( "Spacecraft", "left_aileron" )	

- **Radiation Pressure**

	Returns the value of the radiation pressure that the first body experiences due to the second body.

	.. code-block:: python

		propagation_setup.dependent_variable.radiation_pressure( "Spacecraft", "Sun" )

- **Local Temperature**

	Local temperature within the atmosphere of the **second** body at the position of the **first** body.

	.. code-block:: python

		propagation_setup.dependent_variable.local_temperature( "Spacecraft", "Earth" )
      
- **Local Dynamic Pressure**

	Local dynamic pressure within the atmosphere of the **second** body at the position of the **first** body.

	.. code-block:: python

		propagation_setup.dependent_variable.local_dynamic_pressure( "Spacecraft", "Earth" )
		
- **Local Aerodynamic Heat Rate**

	Local aerodynamic heat rate within the atmosphere of the **second** body at the position of the **first** body.

	.. code-block:: python

		propagation_setup.dependent_variable.local_aerodynamic_heat_rate( "Spacecraft", "Earth" )
		
- **Total Aerodynamic G Load**

	Total aerodynamic G load acting on the **first** body within the atmosphere of the **second** body.

	.. code-block:: python

		propagation_setup.dependent_variable.total_aerodynamic_g_load( "Spacecraft", "Earth" )
		

- **Total Mass Rate**

	Returns the *total* rate of change of the body's mass, e.g. due to thrust.

	.. code-block:: python

		propagation_setup.dependent_variable.total_mass_rate( "Spacecraft" )		

- **Total Torque**

	Returns the *total* torque acting on a body due to all torque model moments in vector form.

	.. code-block:: python

		propagation_setup.dependent_variable.total_torque( "Spacecraft" )
		
- **Total Torque Norm**

	Returns the *norm* of the total torque acting on a body due to all torque model moments, i.e. its scalar value.

	.. code-block:: python

		propagation_setup.dependent_variable.total_torque_norm( "Spacecraft" )

- **Body mass**

	Returns the current mass of a body.

	.. code-block:: python

		propagation_setup.dependent_variable.body_mass( "Spacecraft")
				
- **Body-fixed Cartesian position**

	Returns the current Cartesian position of a body, expressed in the body-fixed frame of a central body.

	.. code-block:: python

		propagation_setup.dependent_variable.central_body_fixed_cartesian_position( "Spacecraft", "Earth" )
		

- **Body-fixed Spherical position**

	Returns the current spherical position of a body, expressed in the body-fixed frame of a central body.

	.. code-block:: python

		propagation_setup.dependent_variable.central_body_fixed_spherical_position( "Spacecraft", "Earth" )
		
- **Airspeed-based velocity**

	Returns the current airspeed-based velocity w.r.t. a central body, expressed in a frame fixed to the central body

	.. code-block:: python

		propagation_setup.dependent_variable.body_fixed_airspeed_velocity( "Spacecraft", "Earth" )
		
- **Groundspeed-based velocity**

	Returns the current groundspeed-based velocity w.r.t. a central body, expressed in a frame fixed to the central body

	.. code-block:: python

		propagation_setup.dependent_variable.body_fixed_groundspeed_velocity( "Spacecraft", "Earth" )
		
- **Periapsis altitude**

	Returns the current periapsis altitude of an orbit, extracted from its current Keplerian state w.r.t. a central body.

	.. code-block:: python

		propagation_setup.dependent_variable.periapsis_altitude( "Spacecraft", "Earth" )

- **Rotation to body-fixed frame - 313 Euler angles**

	Returns the rotation from inertial to body-fixed coordinates, as 313 Euler angles

	.. code-block:: python

		propagation_setup.dependent_variable.inertial_to_body_fixed_313_euler_angles( "Spacecraft" )
		
- **Rotation from Local-Vertical-Local-Horizontal frame**

	Returns the rotation matrix from the Local-Vertical-Local-Horizontal (LVLH) frame w.r.t. a central body to the inertial frame

	.. code-block:: python

		propagation_setup.dependent_variable.lvlh_to_inertial_rotation_matrix( "Spacecraft", "Earth" )
				